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
The share components were imported from react-share. A code snippet for creating the share items in the modal is shown below:

```js
    import {
    EmailShareButton,
    FacebookShareButton,
    TwitterShareButton,
    FacebookIcon,
    FacebookShareCount,
    TwitterIcon,
    EmailIcon
    } from "react-share";
```

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

Clicking on the individual cards, opens a detailed page of the news as below:

<figure class="third">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage1.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage1.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage2.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage2.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage3.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/detailedpage3.PNG"></a>
</figure>

Each of the share icons, when hovered over, show a tooltip:
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/tooltip.png" alt="Tooltip">  <br/>

The user has an option to comment on the the articles.The comment box looks as follows: <br/>
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/comment.PNG" alt="Share Modal">  <br/>

It uses the commentbox from [commentbox.io](https://commentbox.io/docs). A code snippet for creating the comment-box is shown below.

```js
class PageWithComments extends React.Component {

    componentDidMount() {
		this.removeCommentBox = commentBox('5677117685628928-proj');
    }

    componentWillUnmount() {
        this.removeCommentBox();
    }

    render() {
        return (
            <div className="commentbox" id="1"/>
        );
    }
}
```

The articles can be bookmarked for future reference. Bookmarking the articles, adds them to the local storage. Saving them, pops up a toast as shown below:
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/toast.PNG" alt="Toast">  <br/>
Snippet of using local storage:

```js
    localStorage.removeItem("curTab")
	localStorage.setItem("curTab","Home")
```

They can be viewed by clicking on the bookmarks tab.
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/favorite.PNG" alt="Toast">  <br/>
Each of them can be shared, deleted from bookmark or clicked to open the detail page.

The application, also allows to search for news. The news search box also provides an autocomplete.
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/autocomplete.png" alt="Auto-Complete">  <br/>
A code snippet for the search auto complete is shown below:

```js
<div className="searchBOX">
	 <AsyncSelect
          cacheOptions
          loadOptions={
            _.debounce(this.loadOptions, 500, {
              leading: true
            })}
          defaultOptions
		  value={this.state.inputValue=="" ? null : {label:this.state.inputValue, value:this.state.inputValue}}
          onInputChange={this.handleInputChange}
		  onChange={this.onChangeFunc}
		  placeholder='Enter keyword ..'
    />
</div>
handleInputChange = (newValue: string) => {
    const inputValue = newValue.replace(/\W/g, "");
    this.setState({ inputValue });
	console.log(this.state.inputValue)
    return inputValue;
};
onChangeFunc= (optionSelected)=> {
    const name = this.name;
    const value = optionSelected.value;
    const label = optionSelected.label;
	this.props.history.push("/spin")
	this.retrieveCards(value)
	this.setState({inputValue:value});
  }
```
On selecting an item, a page showing the matched news articles appears.
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/searchpage.PNG" alt="Search page">  <br/>
Each of them can shared or clicked to open the detailed page.

A spinner is showed on all the pages, before the data is fetched from the backend.
<img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/spinner.png" alt="Spinner">  <br/>

The website is responsive to the screen sizes.
It is made possible using media queries and react-bootstrap.
Sample code:

```js
<MediaQuery minWidth={768}>
    <div className="smallcardHome" style={{'color':'black'}}>
        <div className="smallcardTitle">
        {this.props.Title} 
            <div className="noMargin" data-toggle="modal" data-target={ids} onClick={this.handleClick}>
                <MdShare/>
            </div>
        </div>
        <div className="smallcardImage">
            <img src={this.props.ImageURL}/>
            <Modal webURl={this.props.WebURL} Title={this.props.Title}/>
        </div>
        <div className="smallcardLower">
            <div className="smallcardDate">
                {curDate}
            </div>
            <div className="smallcardSection" style={{backgroundColor:backGround,color:colorC }}>
                {Sec}
            </div>
        </div>
    </div>
</MediaQuery>
```

```js
import {Navbar, Nav, NavItem, NavDropdown, Form, FormControl, Button} from 'react-bootstrap';
<Navbar className="color-nav" collapseOnSelect expand="lg" >	
    <Nav>
        <div style={{'width':'200px'}}>
            <SearchBox2/>
        </div>
    </Nav>
</Navbar>
```
In a tablet, it looks as below:
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/tablet1.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/tablet1.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/tablet2.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/tablet2.PNG"></a>
</figure>

In a mobile screen, it looks as below:
<figure class="half">
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/mobile1.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/mobile1.PNG"></a>
    <a href="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/mobile2.PNG"><img src="{{ site.url }}{{ site.baseurl }}/images/guardiannewsapp/mobile2.PNG"></a>
</figure>

Link to [github repo](https://github.com/anamay9694/Guardian-NYTimes-NewsApp) for the entire code. 
The project's backend and front-end are hosted at Google App Engine at Google Cloud Platform.

Additional Materials:
1. Guardian News:
[Documentation](https://open-platform.theguardian.com/documentation/)
2. NY Times:
[Site](https://developer.nytimes.com/get-started)
3. React Share:
[Documentation](https://github.com/nygardk/react-share)
4. Comment Box:
[Docs](https://commentbox.io/docs)
5. Microsoft Bing Auto-Suggest
[Site](https://azure.microsoft.com/en-us/services/cognitive-services/autosuggest/)
6. Google Cloud Platform
[Google App Engine](https://cloud.google.com/appengine/docs)
 
