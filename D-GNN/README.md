# Final submission report for GSoC 2023

## Details

|  |  |
| ------------- | ------------- |
| Name  | [Himanshu Chougule](https://github.com/himanshu-02)  |
| Organization  | [INCF](https://summerofcode.withgoogle.com/programs/2023/organizations/incf)  |
| Mentors | [Bradly Alicea](https://bradly-alicea.weebly.com/),  [Jiahang Li](https://github.com/LspongebobJH) [Mayukh Deb](https://github.com/Mayukhdeb) , [Jessie Parent](https://jesparent.github.io/)  |
| Project Title | [D-GNNs: developing DevoGraph for computational developmental biology](https://summerofcode.withgoogle.com/programs/2023/projects/dE4pNOI1) |
| Project page | https://github.com/devoworm/GSoC-2023 |

## Project Description
D-GNNs: developing DevoGraph for computational developmental biology

This project is about using **topological data analysis** over Graph Neural Networks(GNNs) as a method to discover underlying connectivity to characterize a growing network that undergoes shape as well as size transformations for C. elegans. There are two main parts to this project, all of which aim to integrate previous work on embryo networks, developmental connectomes and embryo differentiation.

1. An instance segmentation pipeline 
2. Topological data analysis over stage-2 of DevoGraph to capture the underlying persistence features.  

The instance segmentation task was successfully completed using the watershed algorithm over the semantic segmentation results using DevoLearn. A Mask-RCNN finetuning approach is proposed as well. Topological data analysis was carried out over different microscopy data of the nematode Caenorhabditis elegans. The persistence diagram plots inferred from the C. elegans data is analyzed in their respective notebooks. 

## Instance segmentation 

So what is Instance Segmentation? How is it different from standard segmentation techniques? How is it better for microscopy images? 

**Instance segmentation** is a computer vision task that goes beyond standard segmentation techniques. It involves not only categorizing objects in an image but also distinguishing and delineating individual instances of each object class. It gives us better outputs than standard semantic segmentation techniques by giving us precise object identification for cell counting and tracking. 

Instance segmentation is  achieved by variety of techniques. The methods I researched on were using Mask-RCNN and Watershed segmentation. Mask R-CNN (Mask Region-based Convolutional Neural Network) is a deep learning techniquee used for object instance segmentation, which combines the tasks of object detection and pixel-level image segmentation. It's an extension of the popular Faster R-CNN architecture, with an additional branch for predicting pixel-level masks for each detected object. 

We find the **bounding boxes** of the cells to incorporate it in our Mask R-CNN Pipeline (code given)

![bounding boxes](https://user-images.githubusercontent.com/73215784/277373871-72791140-6eb1-4fdd-a557-956595bbd9f9.png)

**Watershed segmentation** is an image processing technique that identifies object boundaries by treating the image as a topographic map. It works by considering pixels as elevation values and flooding the "landscape" from multiple markers (seed points). Regions associated with the markers are separated by watershed lines, providing a segmentation that can be useful for separating touching objects or delineating structures in an image.

Here are some more outputs!

1. The semantic segmentation image

![devolearn-seg](https://user-images.githubusercontent.com/73215784/277374067-54828569-7cb6-47c2-abec-50b3f868ece7.png)

2. Instance segmentation using **watershed** algorithm

![instance-red-edge](https://user-images.githubusercontent.com/73215784/277374351-7d020498-f44f-4643-af6e-a7776833b0e6.png)

![instance-seg-diff-color](https://user-images.githubusercontent.com/73215784/277374428-bc71e9bd-130f-49a6-a794-20edd7dc2427.png)


## Topological data analysis

Topological data analysis (TDA) is a branch of mathematics and data analysis that aims to uncover the underlying topological properties and features in complex data sets. It is particularly useful for understanding and characterizing the shape, structure, and connectivity of data, especially in high-dimensional spaces.

I applied TDA Concepts mainly persistent homology and lower star filtration on various C. elegans datasets. 

**Persistent homology** is a technique used to study and quantify the topological features of data. The main idea is that we create a series of simplical complexes (Filtration) to represent topological features. Then their homology groups are computed (mathematically theres are the "holes" and connected components in the data). Finally we track the appearence and disappearence of these features and visualize it using a persistence diagram. 

Here are some key outputs!

This is the graph generated using stage 2 of devograph 

![stage2-output](https://user-images.githubusercontent.com/73215784/277400504-bc0238e5-2ac4-4631-9e7b-9d95799d49b9.png)

This is the corresponding **persistence diagram**. For a particular instance of temporal graph dataset the nodes do not change any edge features (the `VietorisRipsPersistence` diagram tends to infinity so we get a unique graph!)

![pd-stage2-graph](https://user-images.githubusercontent.com/73215784/277400720-991dbdf2-ff38-498a-852e-0c93cfd9578f.png)

This is tda on the raw data provided in the dataset folder. We first take the raw data and map it such that we can extract persistence features from it. 

![3d-rawdata](https://user-images.githubusercontent.com/73215784/277385565-91f4c774-928e-4c40-8195-0e639180d1f8.png)

![2d-rawdata](https://user-images.githubusercontent.com/73215784/277385631-14e31e18-ffcc-4126-a62b-bca83f8f1628.png)

![pd-rawdata](https://user-images.githubusercontent.com/73215784/277385739-5ad22b9b-9a65-4ae3-8055-19ffeba7a0c6.png)

Similarly **Lower Star Image Filtration** is used to analyze the topological features. For example it can be used as an approach to identifying the cells even though they have very different shapes.

This is the **persistence diagram** of the above image.

![pd-lower-star](https://user-images.githubusercontent.com/73215784/277385263-6f765317-dc71-4e53-822b-6820e8e16c73.png)

This is the corresponding output of applied lower star filteration. As you can see it can correctly identify the **key features** of our image

![lower-star-filter](https://user-images.githubusercontent.com/73215784/277385369-f9833623-bd74-410e-a021-be913a25c91f.png)

## Future Scope 
- [ ] Working on the MaskRCNN pipeline to give better results.
- [ ] Annotating the dataset used so that it can be used for more complex models that are transformer based.
- [ ] Extracting more tda embeddings over the graphs dynamically


## Conclusion and Acknowledgement 
During the GSoC program, I learned about image segmentation and topological data analysis. It was like going on an exciting research adventure that spanned different fields. Overcoming the challenges was tough but incredibly rewarding. I want to express my sincere thanks to my mentors who were there to guide me every step of the way.  

