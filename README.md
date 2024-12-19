java cINFS2044 Assignment 2 Case Study 
 
In this assignment, you will be developing a system for finding images based on the objects 
present in the images. The system will ingest images, detect objects in the images, and 
retrieve images based on labels associated with objects and by similarity with an example 
image. 
 
Use Cases 
 
The system supports the following use cases: 
 
• UC1 Ingest Image: User provides an image, and System stores the image, identifies 
objects in the image, and records the object types detected in the image in an index. 
 
• UC2 Retrieve Objects by Description: User specifies a list of object types, and the 
system returns the images in its index that match those listed. The system shall 
support two matching modes: 
 
o ALL: an image matches if and only if an object of each specified type is 
present in the image 
o SOME: an image matches if an object of at least one specified type is present 
in the image 
 
• UC3 Retrieve Similar Images: User provides an image, and the system retrieves the 
top K most similar images in order of descending similarity. The provided image may 
or may not already be in the system. The similarity between two images is 
determined based on the cosine similarity measure between the object types 
present in each image. The integer K (K>1) specifies the maximum number of images 
to retrieve. 
 
• UC4 List Images: System shows each image and the object types associated with 
each image in the index. 
 
 
 Example Commands 
 
The following are example commands that the command line frontend of the system shall 
implement: 
 
UC1: 
 
$ python image_search.py add example_images/image1.jpg 
Detected objects chair,dining table,potted plant 
 
$ python image_search.py add example_images/image2.jpg 
Detected objects car,person,truck 
 
$ python image_search.py add example_images/image3.jpg 
Detected objects chair,person 
 
$ python image_search.py add example_images/image4.jpg 
Detected objects car 
 
$ python image_search.py add example_images/image5.jpg 
Detected objects car,person,traffic light 
 
$ python image_search.py add example_images/image6.jpg 
Detected objects chair,couch 
 
UC2: 
 
$ python image_search.py search --all car person 
example_images/image2.jpg: car,person,truck 
example_images/image5.jpg: car,person,traffic light 
2 matches found. 
 
$ python image_search.py search --some car person 
example_images/image2.jpg: car,person,truck 
example_images/image3.jpg: chair,person 
example_images/image4.jpg: car 
example_images/image5.jpg: car,person,traffic light 
4 matches found. 
 
UC3: 
 
$ python image_search.py similar --k 999 example_images/image3.jpg 
1.0000 example_images/image3.jpg 
0.5000 example_images/image6.jpg 
0.4082 example_images/image1.jpg 
0.4082 example_images/image2.jpg 
0.4082 example_images/image5.jpg 
0.0000 example_images/image4.jpg 
 
$ python image_search.py similar --k 3 example_images/image3.jpg 
1.0000 example_images/image3.jpg 
0.5000 example_images/image6.jpg 0.4082 example_images/image1.jpg 
 
$ python image_search.py similar example_images/image7.jpg 
0.5774 example_images/image1.jpg 
 
UC4: 
 
$ python image_search.py list 
example_images/image1.jpg: chair,dining table,potted plant 
example_images/image2.jpg: car,person,truck 
example_images/image3.jpg: chair,person 
example_images/image4.jpg: car 
example_images/image5.jpg: car,person,traffic light 
example_images/image6.jpg: chair,couch 
6 images found. 
 
Other requirements 
 
Input File Format 
 
The system shall be able to read and process images in JPEG format. 
 
For UC2, you can assume that all labels are entered in lowercase, and labels containing 
spaces are appro代 写INFS2044、Python
代做程序编程语言priately surrounded by quotes. 
 
Output Format 
 
The output of the system shall conform to the format of the example outputs given above. 
 
Unless indicated otherwise, the output of the system does not need to be sorted. 
 
For UC3, the output shall be sorted in descending order of similarity. That is, the most 
similar matching image and its similarity shall be listed first, followed by the next similar 
image, etc. 
 
For UC4, the output shall be sorted in ascending alphabetical order. 
 
Internal Storage 
 
You are free to choose either a file-based storage mechanism or an SQLite-based database 
for the implementation of the Index Access component. 
 
The index shall store the file path to the image, not the image data itself. 
 
Object detection 
 The supplied code for object detection can detect ~90 object types. 
 
Future variations 
 
• Other object detection models (including external cloud-based systems) could be 
implemented. 
• Additional object types could be introduced. 
• Additional query types could be introduced. 
• Other similarity metrics could be implemented. 
• Other indexing technologies could be leveraged. 
• Other output formats (for the same information) could be introduced. 
 
These variations are not in scope for your implementation in this assignment, but your 
design must be able to accommodate these extensions largely without modifying the code 
that you have produced. 
 
Decomposition 
 
You must use the following component decomposition as the basis for your implementation 
design: 
 
The responsibilities of the elements are as follows: 
 
Elements Responsibilities 
Console App Front-end, interact with the user 
Image Search Manager Orchestrates the use case processes 
Object Detection Engine Detect objects in an image 
Matching Engine Finds matching images given the object types 
Index Access Stores and accesses the indexed images 
Image Access Read images from the file system 
 
You may introduce additional components in the architecture, provided that you justify why 
these additional components are required. 
 
 Scope  Constraints 
 
Your implementation must respect the boundaries defined by the decomposition and 
include classes for each of the elements in this decomposition. 
 
The implementation must: 
• run using Python 3.10 or higher, and 
• use only the Python 3.10 standard libraries and the packages listed in the 
requirements.txt files supplied with this case study, and 
• not rely on any platform-specific features, and 
• extend the supplied code, and 
• correctly implement the functions described in this document, and 
• it must function correctly with any given input files (you can assume that the entire 
content of the files fits into main memory), and 
• it must include a comprehensive unit test suite using pytest, and 
• adhere to the given decomposition and design principles taught in this course. 
 
Focus your attention on the quality of the code. 
 
It is not sufficient to merely create a functionally correct program to pass this assignment. 
The emphasis is on creating a well-structured, modular, object-oriented design that satisfies 
the design principles and coding practices discussed in this course. 
 
Implementation Notes 
 
You can use the code supplied in module object_detector.py to detect objects in 
images and to encode the tags associated with an image as a Boolean vector (which you will 
need to compute the cosine similarity). Do not modify this file. 
 
You can use the function matplotlib.image.imread to load the image data from a file, and 
sklearn.metrics.pairwise.cosine_similarity to compute the cosine similarity between two 
vectors representing lists of tags. 
 
         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
