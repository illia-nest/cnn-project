<a id="readme-top"></a>


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="120" height="120">
  </a>

  <h3 align="center">AI Project #2: </h3>
  <h3 align="center">Convolutional Neural Network for Image Classification with PyTorch</h3>

  <p align="center">
    by Illia Nesterenko
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#-about-the-project">About The Project</a>
      <ul>
        <li><a href="#-built-with">Built With</a></li>
      </ul>
    </li>
    <li><a href="#-main-findings">Main Findings</a></li>
    <li><a href="#-contacts">Contacts</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## 🔮 About The Project

This project grew from a task from Mike X Cohen's Deep Learning course on Udemy. The goal is to _**train and evaluate a CNN model for image classification on the Fashoin MNIST dataset**_. In short, I have used PyTorch to download the dataset. Then, I normalized it to a range [0,1], put it in Dataloaders, and experimented with model architecture to achieve 90%+ accuracy. Please, look at _cnn-project.ipynb_ for a walkthrough of each phase. For a summary, check <a href="#-training-and-evaluation">Training and Evaluation</a>.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### 🧰 Built With  
[![pytorch]][pytorch-url]  
[![numpy]][numpy-url]  
[![sklearn]][sklearn-url]  
[![matplotlib]][matplotlib-url]  



<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
## 🦾 Training and Evaluation

After the whole web scraping and data preprocessing steps. I have constructed the following graph:

<div align="center">
  <img src="images/graph-full.png" style="height:500px;">
</div>

I analysed it in two ways:

### **1. Using graph analysis metrics (degree and betweenness centality):**

<div align="center">
  <img src="images/degree-one.png" style="height:350px;">
  <img src="images/bet-one.png" style="height:350px;">
</div>

From these pictures, we can see something that it implicitly declared during graph construction: the more interconnected the nodes are the stronger their "gravity force". In other words, the most important (according to the metrics) nodes are in the center. 

<div align="center">
  <img src="images/degree-two.png" style="height:500px;">
</div>

When taking a closer look at the most interconnected points, we can spot an interesting observation. We see that the center of the discourse is constituted from a vocabulary that includes names of states, nations, cities, continents ('ukraine', 'russia', 'russian', 'united states', 'washington','chechen', 'europe', 'european'), international organisations ('united nations', 'un'), and even news outlets ('bbc news'). The striking thing is that among the most interconnected nodes, the only person to be in the list is _vladimir putin_ ('putin'). We didn't find in the list Ukrainian, American or EU member-states leaders. However, I must note that this observation is qualitative and acts more as a "fun fact" than a "hard proof".

### **2. Using clustering algorithms**
As we saw in the previous point, the location of the nodes seems to be meaningful. So, we can try to exploit that and divide nodes into groups. I've experimented with different algorithms (see phase_4.ipynb for full discussion) and arrived at the conclusion that the best one to use is **DBSCAN**:

<div align="center">
  <img src="images/graph-clust.png" style="height:500px;">
</div>

The algorithm divided the nide into 13 groups. Below are examples from group 1 (center of the graph, dark blue on the clustering figure) and group 5 (lower left on the graph, pink on the clustering figure) named "Figure 1" and "Figure 5" correspondingly:

<div align="center">
  <img src="images/figure-one.png" style="height:500px">
  <img src="images/figure-five.png" style="height:500px;">
</div>

The first group is the center that we discussed earlier. But the next group shows us a lot of repeated entities. It seems that spacy's NER model created a lot of near-duplicates that weren't apparent when looking at the table with extracted entities. Yet these near-dupes are specific enough to appear only in one group. This means that the groups are most likely organized around the entities from documents they were extracted and that the repeating entities were pulled from their groups closer to the center. This would explain why the density of the core of the graph is much lower than that of the groups. So, it seems that we built a "map" that shows us from which document the entity is most likely to be from!

<p align="right">(<a href="#readme-top">back to top</a>)</p>




<!-- CONTACT -->
## ☎️ Contacts

Illia Nesterenko - [Telegram](https://t.me/illia_nest) - [LinkedIn](https://www.linkedin.com/in/illianest/) - illia.nest03@gmail.com

Project Link: [https://github.com/illia-nest/web-scrapping-and-ner](https://github.com/illia-nest/web-scrapping-and-ner)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
[numpy]: https://img.shields.io/badge/numpy-%23013343?style=for-the-badge&logo=numpy
[numpy-url]: https://numpy.org/
[matplotlib]: https://img.shields.io/badge/matplotlib-%230C0057?style=for-the-badge&logo=matplotlib
[matplotlib-url]: https://matplotlib.org/
[sklearn]: https://img.shields.io/badge/scikit--learn-%23223228?style=for-the-badge&logo=scikitlearn
[sklearn-url]: https://scikit-learn..org/
[pytorch]: https://img.shields.io/badge/PyTorch-black?style=for-the-badge&logo=pytorch
[pytorch-url]: https://pytorch.org/
