# ReverseImageSearch
This project is a reverse image search on a dataset of over 50,000 shoes. I started by using a smaller dataset of around 40 shoes
to make a version of the reverse image search on my local machine. I used a pretrained neural net (VGG16 or ResNet50) to create 
embeddings for each image in the dataset. Then, I used nearest neighbors (the ball tree algorithm for efficiency) to select the top
k closest images to a search image. Using the smaller dataset, each image in the smaller dataset resulted in itself as the top match,
as expected; however, depending on the neural net or resizing, the other closest matches are subjectively different but nonetheless
resemblant to the original shoe search. I expanded this search to include a larger dataset with 500 images and then I search images 
not within the 500 to show closest matches.

<br>

This process was then implemented in sagemaker. I stored the dataset of 50,000 shoes in an s3 bucket and used ResNet50 to create an
embedding on several thousand of the total set (the instance type can be changed to create an embedding on more images). I stored each
embedding in a csv file which I uploaded to s3. Then, I created a scikit learn model of nearest neighbors where I used the csv file of
points and deployed this scikit learn model in sagemaker.
