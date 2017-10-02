# Introduction

[DeepLab](https://bitbucket.org/aquariusjay/deeplab-public-ver2) is a nice framework for image sematic segmentation. Details about DeepLab please refer the [project website]((https://bitbucket.org/aquariusjay/deeplab-public-ver2)) built by authors.

However, the original package doesn't provide a method to read data from memory. I found there is a little information in the internet to deal with this issue.

If we want to use `MemoryDataLayer` to read the data, it doesnt' work in the case that we want to implement `crf layer`. Thus, I rewrote the `MemoryDataLayer` to make it output 3 top layers so that now we can use it to read data from memory and feed to Caffe module.

We implement common slam techniques to reconstruct the RGB-d mapping. Since the method can't deal with movable objects, we are trying to use semantic segmentation method to remove those objects during mapping (person, cat, car, bus ...). The semantic segmentation library used is [DeepLab-V2](https://bitbucket.org/aquariusjay/deeplab-public-ver2) [VGG-16](http://liangchiehchen.com/projects/DeepLabv2_vgg.html) based model. 

## Tutorial

The example can be found in directory `example_reading_from_memory`. The difference of `MemoryDataLayer` here is that when we call `AddMatVector` function, we should have 3 input. The declaration of function is:

`void MemoryDataLayer<Dtype>::AddMatVector(const vector<cv::Mat>& mat_vector, const vector<int>& labels, const vector<pair<int, int > >& dim_vector)`,
 
where `mat_vector` is the vector for input images, `labels` is the vector for corresponding labels and `dim_vector` is the vector for input images' dimensions. The form of dimensions is `<height, width>`.
