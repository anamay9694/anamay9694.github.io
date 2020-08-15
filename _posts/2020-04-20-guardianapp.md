---
title: "Guardian-NYTimes-NewsApp"
date: 2020-04-20
header:
  image: "/images/rain.jpg"
excerpt: "Web Technologies, JavaScript, React, Node, GCP"
mathjax: "true"
---
**Guardian-NYTimes-NewsApp** is made using JavaScript, React, Node and CSS3.

Project [link](https://reactprojectanamay.wn.r.appspot.com/)

Description:
**Guardian-NYTimes-NewsApp** allows users to search for news using autocomplete, see news articles, share news articles via facebook, twitter or email, navigate to news articles on click, bookmark news articles and also comment on the articles. The front end is responsive to screen sizes.

The main pages from the application:
1. Home Page for Guardian and NY times
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeguardian.png"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeguardian.png"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeny.PNG"></a>
</figure>

2. World Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldny.PNG"></a>
</figure>

3. Politics Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsny.PNG"></a>
</figure>

4. Business Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessny.PNG"></a>
</figure>

5. Technology Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyny.PNG"></a>
</figure>

6. Sports Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/sportsguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/sportsguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/sportsny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/sportsny.PNG"></a>
</figure>

API created in Node for one of the GET requests:
```js
app.get('/getCards/Guardian',(req,res)=>{
	Request.get("https://content.guardianapis.com/search?api-key="+apiKey+"&section=(sport|business|technology|politics)&show-blocks=all", (error, response, body) => {
    if(error) {
        console.log(error);
		res.send(error);
    }
    console.log(JSON.parse(body));
	var to_send=JSON.parse(body);
	res.send(to_send);
});
});
```
Code snippet handling the call request from React front-end:
```js
class BodyCards extends React.Component{
	constructor(){
		super()
		this.state={
			name:"Anamay",
			counter: 0,
			data:{},
			didReceive: false
		}
		this.refresh=this.refresh.bind(this)
	}
	refresh(){
		console.log("Refresh Called:")
		this.setState({didReceive:false})
	}
	componentDidMount(){		
		this.refresh()
		var pap=this.props.paper
		fetch("https://nodeanamayproject.wn.r.appspot.com/getCards/"+pap)
		.then(response=>response.json())
		.then(dataset=> {
			this.setState({
			data:dataset,
			didReceive:true
		})
		})
	}
```


