---
layout: post
title: 'What makes something #beautiful?'
date: '2014-06-15 19:20:00'
---

I think it was in high school, in an English Literature lesson, someone was droning on about how “beauty is in the eye of the beholder”, how beauty is an experience of the individual, that anything can be beautiful if someone considers it so. In some ways this is a nice idea, a free and easy way to understand the beauty around us, but is it true?

After all, if beauty is entirely subjective, a product of individual preference, why is it so consistent? Scarlett Johansson is universally seen as beautiful, as are sunsets, vistas and diamonds. 

To understand how people see beauty today, I analyzed a 1000 pictures [tagged #beautiful on Instagram](http://iconosquare.com/tag/beautiful/). 

## Describing pictures

To analyze 1000 pictures by hand is error prone and time consuming. So to get an overview of what people considered beautiful, I tagged the images using a [machine vision API created by Alchemy](http://www.alchemyapi.com/products/features/image-tagging/). The machine vision API works somewhat like facial recognition software. It looks at an image and returns a list of tags, saying what it thinks the image contains. For example, [this image](http://demo1.alchemyapi.com/images/vision/emaxfpo.jpg) is 99% likely to contain a cat, 57% likely to contain an animal and so on. 

So what was contained within our 1000 #beautiful images?

<iframe style="width: 100%;
height: 500px;
border: 1px solid #DEDEDE;" src="http://bl.ocks.org/richshaw/raw/0a7a1dd78bf1882c67fa/" marginwidth="0" marginheight="0" scrolling="no"></iframe>

The bubble chart above shows the number of times each tag occurred. I don’t want to conclude that, as humans, we are a race of narcissists, but we do have a lot of beautiful people, but also some sunsets, sky and sport.

We can also look at an average of images for different tags to see if there’s any consistency in color and composition of the images. 

![What is beautiful? Average person](/assets/beautiful-average/person.jpg)
<p style='text-align: center;'>Average #beautiful person</p>

![What is beautiful? Average girl](/assets/beautiful-average/girl.jpg)
<p style='text-align: center;'>Average #beautiful girl</p>

![What is beautiful? Average model](/assets/beautiful-average/model.jpg)
<p style='text-align: center;'>Average #beautiful model</p>

![What is beautiful? Average sport](/assets/beautiful-average/sport.jpg)
<p style='text-align: center;'>Average #beautiful sport</p>

![What is beautiful? Average nature](/assets/beautiful-average/nature.jpg)
<p style='text-align: center;'>Average #beautiful nature</p>

![What is beautiful? Average flower](/assets/beautiful-average/flower.jpg)
<p style='text-align: center;'>Average #beautiful flower</p>

![What is beautiful? Average sunset](/assets/beautiful-average/sunset.jpg)
<p style='text-align: center;'>Average #beautiful sunset</p>

![What is beautiful? Average cat](/assets/beautiful-average/cat.jpg)
<p style='text-align: center;'>Average #beautiful cat</p>

The average images were created by taking the average pixel color, for each pixel across all the images of a tag. Much like numeric averages, average images don’t tell us much about the overall structure of the data but give us a single point of reference for commonalities within the data. In this case the average images give us a feel for the common composition and colors used within the images.     

While the bubble chart and averages tell us about the common tags, it doesn’t tell us anything about how the tags relate to each other. What is related to “people”? What sports are included in “sport”?

<iframe style="width: 100%;
height: 500px;
border: 1px solid #DEDEDE;" src="http://bl.ocks.org/richshaw/raw/b7f99f539e2a2546ab64/" marginwidth="0" marginheight="0" scrolling="no"></iframe>

The network graph above shows how the tags fit together. Each circle represents a tag, and a line is draw between tags that are mentioned together. We can see that beautiful flowers include “orchid,” “poppy” and “dandelion” and sports like “football,” “golf” and even “wrestling” have beautiful moments. We can also look at the overall structure of the graph. You’ll see that there are four clusters of circles, one centering on people, one on animals, another on nature and a fourth on buildings (pulled close to nature by the sun and the sky).

We can combine the data from the bubble chart and the network graph, along with a [segmentation](http://arxiv.org/pdf/physics/0602124.pdf) to give us a complete overview of the tags.

![What is beautiful? Graph](/assets/beautifulgraph.svg)

In the network graph above, the size of the circles and text show how many times a tag was used, like in the bubble chart. The lines show which tags are mentioned together, while the thickness of the lines represents how often the tags were mentioned together. The colors show the results of our segmentation. There are clusters of images around beautiful people, animals, flowers, sky and buildings.

## Who are the beautiful people?

Pictures of people seem to dominate what people perceive as beautiful. But what makes these people beautiful? Is it their hair? Their eyes? What is it?

To find out, I recruited a team of humans to analyze the images tagged with “person.” Each analyst had to answer a sequence of questions describing the properties of the images: Does the image contain a person? (The computer could have tagged incorrectly.) How long is their hair? What color is it? And so on. 

The plot below shows an analysis of the different properties of the beautiful people images and how they relate to each other. The properties toward the center of the plot are the ones mentioned most frequently, and the properties that are close to each other tend to appear together.

![Mulitple Correspondence Analysis Plot](/assets/MCA.svg)

The plot shows us that an image of a person is more likely to be #beautiful if they’re young, white, females with a happy facial expression. The YWFH’s accounted for a full 23% of all images of #beautiful people, significantly higher than any other group. It also doesn’t hurt if you’re a brunette. Brunettes account for 72% of #beautiful people overall, and young, white, females with a happy facial expression and long brunette hair make up 10% of #beautiful people overall. 

## Jolie laide
I’m disappointed. I never expected beauty to entirely be beholden to the beholder, but I never expected to find this level of conformity. Almost half of #beautiful pictures on Instagram are of people, and about 1 in 4 of those people photographed display the same features. While typically it’s the media that has promoted a certain standards of beauty, it’s not the media outlets posting these photos. 

[Over 90% of Instagram users or people aged 18-35](http://www.businessinsider.com/instagram-demographics-2013-12). Part of me (the part that watched a lot of Bill Hicks at college, wastes its time watching reruns of House and follows @neinquarterly) wants to conclude the narcissism and conformity displayed on Instagram are a malaise of a generation. 

But that’s it’s not that simple. That conclusion is too broad. Aristotle, Plato, Kant and Locke all failed to develop a definitive definition of beauty because beauty doesn’t have a single definition, but nor is it entirely subjective.

The best explanations of what make sometime beautiful are relative. [In Beauty, Roger Scruton](http://www.amazon.com/gp/product/0199229759/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0199229759&linkCode=as2&tag=richshaw-20) sees beauty as a rational judgment by the individual, that rationality has to draw up experience on the world around them. Similarly, [Crispin Sartwell in Six Names of Beauty](http://www.amazon.com/gp/product/0415979927/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0415979927&linkCode=as2&tag=richshaw-20) sees beauty defined by the relationship between the observer, the observed and the environment around them.   

With this in mind, the #beautiful people of Instagram seem less malevolent. Uploading a picture to Instagram is a social interaction between the uploader and the other members of Instagram. Social interactions are rarely neutral. They have a purpose. 

For some, Instagram is a game of “likes.” The more “likes” your image gets, the better, and using popular tags like #beautiful can help with that. Others use Instagram as a way to display their perfectly curated life to friends, and #beautiful is a statement of an aspirational self-image. 

Instagram photos are a product of the platform and the sample I used for the research. Instagram is a US-based company and is popular on its home turf. I also sampled images that were tagged #beautiful not [#precioso](http://iconosquare.com/tag/precioso/), [#belo](http://iconosquare.com/tag/belo/) or [아름다운](http://iconosquare.com/tag/%EC%95%84%EB%A6%84%EB%8B%A4%EC%9A%B4/). If I had looked at beautiful in different languages, I would have discovered something different. 

While differences between languages wouldn’t be surprising, what is surprising is the amount of homogeneity within our US leading, english tagged #beautiful images. 

So was suffering through high school English literature worth it? Is “beauty is in the eye of the beholder”? If it is, then with certain people in certain places a lot of us look through the same eye.


## Resources

* Bubble chart code: http://bl.ocks.org/richshaw/0a7a1dd78bf1882c67fa
* Network graph code: http://bl.ocks.org/richshaw/b7f99f539e2a2546ab64
* Pretty tables: http://bl.ocks.org/richshaw/raw/187f2f6df9b3f5ed55b8/ 
* Data: https://drive.google.com/folderview?id=0B268p6viJlBMaUxmUlF6TDZiOUU&usp=sharing




