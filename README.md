# Scalable duplicate detection using Locality Sensitive Hashing

For an assignment of the course; Computer Science at the Erasmus University in Rotterdam, students were asked to address the scalability issue for duplicate product detection using data coming from several Web shops. 

The dataset is available on: https://personal.eur.nl/frasincar/datasets/TVs-allmerged.zip as a JSON file that contains 1,624 descriptions of televisions coming from four Web shops, namely Amazon.com, Newegg.com, Best-Buy.com, and TheNerds.net. For every television, the shop, the title, modelID and a set of key-value paired features is provided. The modelID is the golden standard for finding the duplicates, and is therefore withheld from the proposed algorithm for finding the duplicates when testing. This is also in line with reality, since modelID is often missing on many Websites, which makes finding duplicates from product information an interesting problem. 

The structure of the code is as follows;

Firstly, the data is preprocessed. In the title and the value parts of the key-value pairs that represent the features, every variation of 'inch', namely '"', 'Inch', '-inch', ' inch', 'inch' and 'inches', is replaced by 'inch'. The same is done for variations of 'herz'. Next, a product representation for LSH is formed. In this project, I chose to include, for every product, model words of the title, the first word of the title, and model words of the value part of features. These 'tokens' are then used to create binary vectors representing the products. Next, these binary vectors are used to create a signature matrix with minhashing. Minhashing is a technique that reduces large, and often sparse, binary vectors to signature vectors using a hash function. In our case, the hash functions are of the form (a + bx)mod(p), where a and b are random integers and p a random prime number. The final goal of these signatures is to compare them and to give an accurate and fast estimation of the Jaccard similarity of two sets. This Jaccard similarity is then compared to a threshold value for different numbers of bands (b) and rows (r). LSH divides the signature matrix M into bands b and rows r. r and b are chosen in such a way that r * b = dim(M). In addition, the relationship between false positives and false negatives can be represented by the the threshold value t. t can be approximated by (1. / b) ** (1. / r)
