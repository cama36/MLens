# MLens
## Dataset introduction:
MLens is a lens 3D data obtained by scanning in a real factory environment using OCT technology. It is also the first open dataset that applies OCT technology to the field of transparent lens defect detection. All data has been retained in its original scanned form without any processing (resulting in a very large dataset :)). Given that most defects are typically very small in scale, it is essential to design robust data processing algorithms that effectively minimize redundant noise while retaining critical defect points. This necessity underlines our decision to provide the original, unprocessed data, despite the resultant dataset size. Our aim is to empower users with a comprehensive understanding of the original data, facilitating the development of innovative data processing algorithms tailored to their specific needs.
## Mlens example structure  
<pre>
├── Mlens
│   ├── ProductA
│   │   │── NG
│   │   │   │── Data
│   │   │   │── Annotation_A.pkl #annotation label of product A.
│   │   │── G
│   ├── ProductB
│   │   │── NG
│   │   │   │── Data
│   │   │   │── Annotation_B.pkl #annotation label of product B.
│   │   │── G
├── README.md
</pre>
## Mlens public 
The entire data set will be made public after cvpr review.

## Pre-process:
The following outlines our data preprocessing methods. It is important to note that the current approaches may not be optimal, and we encourage everyone to start from the original data to propose more suitable methods.

### In product A：  
1.the Z-axis values within the region containing the lens range from 70 to 400. As part of the data preprocessing, the starting Z value of 70 will be shifted to 0. Specifically, for the raw data segment where z>330, it is necessary to first extract the Z-axis values falling within the 70–400 range. After extraction, the values should be offset so that 70 corresponds to 0. Apologies for the inconvenience caused; however, this adjustment should be relatively straightforward.  
2.Use an intensity threshold of 150 to filter out high-intensity point clouds, reducing the number of point clouds while clearly retaining the boundaries between the lens and the pallet.  
3.Generate a bev perspective gray-image of the point cloud, mark the "saturation artifact" and lens area, and use a 2D model to segmentation. Finally, map the ROI area extracted from 2D (a pillar in the 3D perspective) back to the point cloud to achieve data cropping of the point cloud.


### In product B:
1.the provided raw Z-axis values lie within the range of 0 to 1024. However, during the data preprocessing stage, only the range from 0 to 500 is utilized, as this region encompasses the majority of the lens area.  
2.The intensity threshold used is 120, and the rest remains the same as product A.
