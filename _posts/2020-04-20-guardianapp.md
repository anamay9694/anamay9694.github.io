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
+ Home Page for Guardian and NY times
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeguardian.png"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeguardian.png"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/homeny.PNG"></a>
</figure>

+ World Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/worldny.PNG"></a>
</figure>

+ Politics Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/politicsny.PNG"></a>
</figure>

+ Business Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/businessny.PNG"></a>
</figure>

+ Technology Page for Guardian and NY times 
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyguardian.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyguardian.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyny.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/technologyny.PNG"></a>
</figure>

+ Sports Page for Guardian and NY times 
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
Each of the news articles can be shared.
Clicking on the share button, opens a modal as shown below. It has the options to share via facebook, twitter and email. <br/>
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/modalshare.PNG" alt="Share Modal">  <br/>
The share components were imported from react-share. A code snippet to creating the share items in the modal is shown below
```js
<div className="Icons">
    <div className="Facebook">
        <FacebookShareButton url={this.props.webURl} hashtag={"#CSCI_571_NewsApp"} >
            <FacebookIcon size={60} round={true}/>
        </FacebookShareButton>
    </div>
    <div className="Twitter">
        <TwitterShareButton url={this.props.webURl} hashtags={["CSCI_571_NewsApp"]}>
            <TwitterIcon size={60} round={true}/>
        </TwitterShareButton>
    </div>
    <div className="Email">
        <EmailShareButton url={this.props.webURl} subject={"#CSCI_571_NewsApp"}>
            <EmailIcon size={60} round={true}/>
        </EmailShareButton>
    </div>
</div>
```

Clicking on the indivual cards, opens a detailed page of the news as below:

<figure class="third">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage1.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage1.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage2.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage2.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage3.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage3.PNG"></a>
</figure>

