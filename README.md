# Article-some-project
Project
APIs are mechanisms that enable two software components to communicate with each other using a set of definitions and protocols
Covid_19 API how it work
One advantage of using the COVID-19 API is that it provides up-to-date information on the number of cases, deaths, and recoveries from COVID-19 around the world. This data can be used to create visualizations or tables that can help people understand the scope of the pandemic and track its progress over time. Additionally, the API provides data on a country-by-country basis, which allows users to compare the situation in different parts of the world and identify trends and patterns.
To draw a Highchart using data from the COVID-19 API, you can use the $.getJSON() method to retrieve the data and then create a chart based on that data. Here is an example:
// fetch data from the COVID-19 API and return selected attributes
function fetchData() {
    return fetch("<https://api.covid19api.com/summary>") 
      .then((response) => response.json())
      .then((data) => {
        const countries = data.Countries.map((country) => {
          return {
            name: country.Country,
            cases: country.TotalConfirmed,
            deaths: country.TotalDeaths,
            recovered: country.TotalRecovered,
          };
        });
        return countries;
      })
      .catch((error) => {
        console.error("Failed to fetch COVID-19 data:", error);
      });
  }
  
  // Create the chart
  function createChart(country) {
    const chart = Highcharts.chart("chart-container", {
      chart: {
        type: "column",
      },
      title: {
        text: country.name + "'s summary",
      },
      xAxis: {
        type: "category",
      },
      yAxis: {
        title: {
          text: "Number of Cases",
        },
      },
      legend: {
        enabled: false,
      },
      plotOptions: {
        series: {
          borderWidth: 0,
          dataLabels: {
            enabled: true,
            format: "{point.y}",
          },
        },
      },
      series: [
        {
          name: "Cases",
          colorByPoint: true,
          data: {
            name: country.name,
            y: country.cases,
            drilldown: country.name,
          },
        },
      ],
    });
    chart.addSeries({
      name: country.name,
      id: country.name,
      type: "column",
      data: [
        ["Deaths", country.deaths],
        ["Recovered", country.recovered],
      ],
    });
  
    return chart;
  }
  
  // Search for specific country
  function searchForCountry(countries, chart) {
    const searchBox = document.querySelector("#search-box");
    searchBox.addEventListener("input", (event) => {
      const searchTerm = event.target.value.toLowerCase();
      console.log("searchTerm", searchTerm);
      const matchingCountries = countries.filter((country) => {
        return country.name.toLowerCase().includes(searchTerm);
      });
      chart.series[0].setData({
        name: matchingCountries[0].name,
        y: matchingCountries[0].cases,
        drilldown: matchingCountries[0].name,
      });
      chart.setTitle({ text: matchingCountries[0].name + "'s summary" });
    });
  }
  
  // Select country
  function selectCountry(countries, chart) {
    const selectBox = document.querySelector("#country-select");
    countries.forEach((country) => {
      const option = document.createElement("option");
      option.value = country.name;
      option.textContent = country.name;
      selectBox.appendChild(option);
    });
    selectBox.addEventListener("change", (event) => {
      const selectedCountry = event.target.value;
      console.log("selectedCountry", selectedCountry);
      const matchingCountry = countries.find((country) => {
        return country.name === selectedCountry;
      });
      chart.series[0].setData([
        {
          name: "Cases",
          y: matchingCountry.cases,
          drilldown: matchingCountry.name,
        },
      ]);
      chart.setTitle({ text: matchingCountry.name + "'s summary" }); // update chart title
    });
  }
  
  async function main() {
    const countries = await fetchData();
    const chart = createChart(countries[0]);
    searchForCountry(countries, chart);
    selectCountry(countries, chart);
  }
  
  main();
  init()
  function init(){
      var url =" <https://api.covid19api.com/summary> "
      
      var data =""
      
      $.get(url,function(data)
      {
          console.log(data.Global)
          data =`
<td>${data.Global.TotalConfirmed}</td>
<td>${data.Global.TotalDeaths}</td>
<td>${data.Global.TotalRecovered}</td>
<td>${data.Global.NewDeaths}</td>
<td>${data.Global.NewConfirmed}</td>
<td>${data.Global.Date}</td>
 `
 
 $("#data").html(data)
      }
      
      
     
      
      
      )
      function refreshData(){
          clearData()
          init()
      }
      function clearData(){
          $("#data").empty()
        
      }
      var data = "";
fetch(url)
.then((response) => response.json())
.then((data) => {
console.log(data);
for (let i = 0; i < data.Countries.length; i++) {
col = `
<tr>
<td>${data.Countries[i].Country}</td>
<td>${data.Countries[i].TotalConfirmed}</td>
<td>${data.Countries[i].TotalDeaths}</td>
<td>${data.Countries[i].TotalRecovered}</td>
<td>${data.Countries[i].NewDeaths}</td>
<td>${data.Countries[i].NewConfirmed}</td>
<td>${data.Countries[i].Date}</td>
</tr>
`;
document.querySelector("#tbl").innerHTML+=col;
}
})
      }
function refreshData(){
          clearData()
          init()
      }
      function clearData(){
          $("#data").empty()
        
      }
This code creates a column chart showing the total number of COVID-19 cases by country, using data from the COVID-19 API. You can customize the chart by changing the chart and title options, as well as the xAxis, yAxis, and series options to suit your needs.

To create a table using API data, you can use JavaScript and HTML. First, use the fetch() method to retrieve the data from the API. Then, parse the data into an array of objects that can be used to populate the table. Finally, use HTML to create a table and insert the data into the table.
Here is an example of how to create a table using data from the COVID-19 API:
<table>
  <thead>
    <tr>
      <th>Country</th>
      <th>Total Cases</th>
      <th>Total Deaths</th>
      <th>Total Recovered</th>
      <th>New Deaths</th>
      <th>New Cases</th>
      <th>Date</th>
    </tr>
  </thead>
  <tbody id="data">
  </tbody>
</table>
const url = "<https://api.covid19api.com/summary>";
fetch(url)
  .then(response => response.json())
  .then(data => {
    const tableData = data.Countries.map(country => {
      return `
        <tr>
          <td>${country.Country}</td>
          <td>${country.TotalConfirmed}</td>
          <td>${country.TotalDeaths}</td>
          <td>${country.TotalRecovered}</td>
          <td>${country.NewDeaths}</td>
          <td>${country.NewConfirmed}</td>
          <td>${country.Date}</td>
        </tr>
      `;
    });
    document.getElementById("data").innerHTML = tableData.join("");
  })
  .catch(error => {
    console.error("Failed to fetch COVID-19 data:", error);
  });
Movies_API
To fetch data from the Movies API, we use the fetch() method, which is a built-in JavaScript method for making HTTP requests. We can define the URL of the API endpoint we want to fetch data from, and then call the fetch() method with this URL as an argument. The fetch() method returns a promise that resolves to a Response object. We can then call the json() method on this Response object to extract the JSON data from the response.
After extracting the data, we can use it to do something useful, such as displaying it on a webpage or processing it further. In the example provided, the extracted data is used to create a list of the most popular movies, including their title, year of release, and rating. The list is displayed on a webpage using HTML and CSS.
One advantage of using APIs like the Movies API is that they provide a way to access a large amount of data quickly and easily. This data can be used for a variety of purposes, such as creating informative visualizations, building recommendation systems, or conducting market research. Additionally, many APIs are free or low-cost, making them accessible to developers and businesses of all sizes.
To fetch data from the Movies API, you can use the fetch() method, which is a built-in JavaScript method for making HTTP requests. Here is an example:
const url = "<https://api.movies.com/movies>";
fetch(url)
  .then(response => response.json())
  .then(data => {
    // do something with the data
  })
  .catch(error => {
    console.error("Failed to fetch movies data:", error);
  });
fetch("<https://imdb-api.com/API/MostPopularMovies/k_8v3u2v40>")
 .then((response) => response.json()) 
 .then((objectData) => { 
// ///  console.log(objectData); 
  for (let i = 0; i < 40; i++) { 
    let card = `<div class="col-lg-2 col-md-3 col-sm-4 col-6"> 
       <a href=""> 
        <div class="card cards border-0"> 
           <img src="${objectData.items[i].image}" class="img-fluid rounded-3" alt="" width="100%" /> 
         </div> 
     </a> 
       <p class="fw-bold m-0 mt-1 ms-1" style="font-size: small">  ${objectData.items[i].title} </p> 
       <p class="text-muted"> 
         ${objectData.items[i].year}  
        <span class="badge bg-secondary float-end">${objectData.items[i].imDbRating}</span> 
      </p> 
     </div>`; 
     document.getElementById('movie').innerHTML += card; 
 }; 
 }) 
 .catch((err) => console.error(err));
  
function Movie() {
 
  
  var title = document.querySelector("#searchId");
  alert(title.value);
  const urlSearchMovies = `https://imdb-api.com/en/API/SearchAll/k_8v3u2v40/${title.value}`;
  fetch(urlSearchMovies)
    .then((response) => response.json())
    .then((Movies) => {
      for (let i = 0; i < Movies.results.length; i++) {
        console.log(Movies.results[i])
        let card = `<div class="col-lg-2 col-md-3 col-sm-4 col-6">
        <button class="cards border-0 rounded shadow-lg"style="width: 170px;height: 260px;background-image: url(${Movies.results[i].image});  background-size: cover; background-position: center;"
        value="${Movies.results[i].id}" onclick="getID(this.value)">
        </button>
        <p class="fw-bold m-0 mt-1 ms-1" style="font-size: small">
          ${Movies.results[i].title}
        </p>
        <p class="text-muted">
         
          <span class="badge bg-secondary float-end"></span>
        </p>
      </div>`; 
       document.getElementById('searchnew').innerHTML+=card;
      }
    })
  .catch(err=>console.error(err))
}
In this example, we first define the URL of the API endpoint we want to fetch data from. We then
call the fetch() method with this URL as an argument. The fetch() method returns a promise that resolves to a Response object. We can then call the json() method on this Response object to extract the JSON data from the response.
We can then use the extracted data to do something useful, such as displaying it on a webpage or processing it further. If there is an error while fetching the data, we can catch the error using the catch() method and log an error message to the console.

equb 
How to Create Page an EPUB using HTML,CSS ,Javascrpt and Bootstrap

An EPUB file is the other type of ebook file that is popular. If you are planning on writing or publishing an ebook, you should save your HTML as a Mobipocket file, and also as an EPUB. In some ways, an epub file is a lot easier to build than a Mobi file. Since EPUB is based on HTML &CSS you simply need to create your HTML files, collect them together, and call it an epub.
These are the steps you should take to create an epub file:
Build your HTML. Your book is written in HTML, with CSS for styling. But, it's not just HTML, it's HTML. So, if you don't normally write in XHTML (closing your elements, using quotes around all attributes, and so on) you will need to convert your HTML to XHTML. You can use one or more HTML files for your books. Most people separate the chapters into separate XHTML files. Once you have all the HTML files, put them in a folder all together.
Create a MIME Type File. In your text editor, open a new document and type:

application/epub+zip

Add your style sheets. You should create two style sheets for your book one for the pages called
page_styles.css

<style>
   
        .container{
          
        padding-bottom: 50px;
        }
        .card{
          margin: 20px;
          background-color: darkgray;
          border-radius: 15px;
        }
        .namee{
          text-align: center;
        }
        .list{
          margin: 30px;
          border-radius: 10px;
          border-style: double;
          border-color: black;
          background-color: darkgray;
        }
        h2{
          color: #000;
       }
        
    </style>
Build your title page. You don't have to use the cover image as your title page, but most people do. To add your title page, create an HTML file called
titlepage.html

The first step is to build the skeleton of the website that the user interacts with. To build the skeleton, we used a framework commonly known as Bootstrap. In the following image we can see how we call the link for the bootstrap framework.
<link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
      crossorigin="anonymous"
    />
<script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM"
      crossorigin="anonymous"
    ></script>
After linking our site to the boot site, we started creating the registration form and accepting information about our users. After the user enters their details and clicks the submit button, the form is checked to see if it's valid or invalid. And the method we use to validate these forms is very simple, which is if the input field is empty or if there's a syntax error and the user clicks the submit button, it gives us an error message. And this is done using the if-else method on the JavaScript code. this is the equb interface
And it will add our amount of registration, it will tell us the winner and it will pop up in the top, it will contain all our information.
function fn1(){
        var  username= document.getElementById("firstName").value;
        var  LastName= document.getElementById("LastName").value;
        var  amount= document.getElementById("amount").value;
         
        
        const table = document.getElementById("tbb");
        var row=table.insertRow();
        var cell=row.insertCell(0);
        var cell1=row.insertCell(1);
        var cell2=row.insertCell(2);
 
        cell.innerHTML = username;
        cell1.innerHTML = LastName;
        cell2.innerHTML = amount;   
        
        sum+= Number(amount);
        nameOfUser.push(username + " " + LastName);
        lengthEqub++;
 
 }
The code starts with a function called fn1(), which takes two parameters, username and amount.
The first parameter is the value of an input element on the page, identified by its id attribute as "first Name".
The second parameter is the value of another input element on the page, identified by its id attribute as "LastName
const sum+= Number(amount); This row adds up all the numbers in amount to get their total value.
This number will later be the basis for the calculation of how much money has been spent in that wallet during that transaction.
The code is a JavaScript function that takes the value of the FirstName and LastName inputs, as well as the Amount input.
It then inserts a row into the table with three cells: FirstName, LastName and Amount.
The sum variable is incremented by adding Number(amount) to it.
function gen() {
              var ran = Math.floor(Math.random() * lengthEqub);
                      
    var winnerName = nameOfUser[ran];
 alert("In this round the winner is  :   "+ winnerName + " " + sum );
          
  
  }
The code is a function that generates a random number then alerts an alert box with that person's name and total score.
This function has one parameter, length Equb, which is used as input for generating random numbers. we have assigned values to variables called ran and winner Name respectively.
We then use these variables in an alert box to inform us who has won this round and how much they have scored so sum
The code generates a random number from 0 to the length of the nameOfUser array
If the value is found, then the message "In this round the winner is : "+ winner Name + " " + sum.

Folder Structure
We will now start working on creating the portfolio website.
First, let's create the folder structure. You can get the project starter files on GitHub. Also, you can visit here to see the live demo of this project.
The folder structure consists of index.html, style.css, and script.js files and an images folder. We'll write all CSS in the style.css file and the JavaScript in the script.js file .
In the index.html file, you can see the HTML boilerplate code with the Bootstrap CDN, font awesome kit, and a link to the external style sheet and JavaScript.
Here, the script.js file is loaded after loading all the HTML code.
How to Add a Navigation Menu to Your Portfolio

We will use Bootstrap's fixed-top class in nav element to keep the navbar at the top of the page. The navbar also has a navbar-brand class where we keep the name of the person as a brand.
<nav class="navbar navbar-expand-lg fixed-top navbarScroll">
        <div class="wrapper">
  <div class="whole-img">
  <header class="primary-header flex">
   <!-- <div class="nav-holder flex"> -->
    <!-- <div class="logo">
     <img src="images/logo.jpg" alt="personal logo">
    </div> -->
    <button class="button-toggle" aria-controls="primary-navigation" aria-expanded="false">
     <span class="sr-only"></span>
    </button>
    <nav>
     <ul id="primary-navigation" data-visible="false" class="primary-navigation flex">
      <li class="active"><a href="#home"><span style="color: rgb(255, 255, 255);" aria-hidden="true">Home</span></a></li>
      <li><a href="#about"><span style="color: rgb(255, 255, 255); aria-hidden="true">About</span></a></li>
      <li><a href="#My Skil"><span style="color: #fff;" aria-hidden="true">My Skil</span></a></li>
      <li><a href="#projects"><span style="color: #fff;" aria-hidden="true">Projects</span></a></li>
      <li><a href="#contact" class="contactbtn"><span aria-hidden="true">Contact</span></a></li>
     </ul>
    </nav>
   <!-- </div> -->
  </header>
  
   <div class="hero" id="home">
    <div class="herotext">
     <h1><div class="first-txt">I'am Hayat Hussen<span style="color:#09f9f9; text-shadow: 5px 2px 8px rgb(29, 198, 190);"> future</span> together<span style="color: red"></span> !!!</div></h1>
    </div>
   </div>
  </div>
   <div class="body-content">
    <div class="intro">
     
    <h2 class="about" id="about">A little bit about Hayat Hussen</h2>
      <div class="line1"></div>
     <p>My name is Hayat Hussen , I'm a Web Developer, I aiming to create beautiful and functional websites.and iam Archtecher and i do home design .That is why i enrolled at Act American college .and I am currently a third year student After finshing my BSc which my then i become a pagrammmer and web Developer
     </p
    </div>
    
    </div>
    </nav>
Add your style sheets. You should create two style sheets for your book one for the pages called
page_styles.css
<style>
   /* changing the link color */
a:link,
a:visited,
a:hover {
	color: #21053b;
	text-decoration: none;
}

/* smoothing teh scroll */
html {
	scroll-behavior: smooth;
}

/* no borders on the page */
body {
	margin: 0;
	overflow-x: hidden;
}

/* taking the whole page */
.wrapper {
	width: 100%;
	height: 100%;
	background-color: #eee;
}
.card{
    width: 1px;
    height: 1px;
}

.font-face{

	src:url("../res/font/D-DIN.otf");
	font-family: d-din;
	

}

.do{
	margin-top: 0;
	position: relative;
  
  }
  .do .look{
	
	margin-top: 0;
  }
  .abouts{
	
	border-style: groove;
  width: 70%;
  border: 2px solid white;
	border-radius: 12px;
	padding: 5px;
	margin-bottom: 10px;
  }
  .abouts p{
	font-family: 'Josefin Sans', sans-serif;
  font-size: large;
  color: indianred;
  
  }
  .look h2{
	color: brown;
	font-size: 75px;
	text-transform: capitalize;
	margin-bottom: 20px;
  }
  
  .ok div{
	color: hotpink;
	border-style: groove;
  border-color: black;
  border: 2px solid brown;
	border-radius: 12px;
	padding: 5px;
	width: 0%;
   
	
  } 
  .ok{
	background-color: indianred;
	width:500px;
	border-radius: 5px;
	border: 2px solid ;
	border-radius: 12px;
   
	margin: 5px;
  }
  .ok div span{
	height:40px;
	width:40px;
	border-radius:50% ;
	background:#fff;
	float:right;
	margin-top:-15px;
	margin-right: -20px;
	color: #333;
	display: flex;
	align-items: center;
	justify-content: center;
  }
  
  .ok .one{
	background: brown;
	animation:one 1s linear forwards;
  }
  .ok .two{
	background: brown;
	animation:two 1s linear forwards;
  }
  .ok .three{
	background: brown;
	animation:three 1s linear forwards;
  }
  .ok .five{
	background: brown;
	animation:five 1s linear forwards;
  }
  .ok .six{
	background: brown;
	animation:six 1s linear forwards;
  }
  .ok .seven{
	background:brown;
	animation:seven 1s linear forwards;
  }
  
  .ok .one span{
	border:1px solid white;
  
  }
  .ok .two span{
	border:1px solid white;
  }
  .ok .three span{
	border:1px solid white;
  }
  .ok .five span{
	border:1px solid white;
  }
  .ok .six span{
	border:1px solid white;
  }
  .ok .seven span{
	border:1px solid white;
  }
  @keyframes one{
	100%{
	  width:40%;
	}
  }
  @keyframes two{
	100%{
	  width:70%;
	}
  }
  @keyframes three{
	100%{
	  width:80%;
	}
  }
  @keyframes five{
	100%{
	  width:90%;
	}
  }
  @keyframes six{
	100%{
	  width:95%;
	}
  }
  @keyframes seven{
	100%{
	  width:50%;
	}
  }
  .menu-icon{
	width:25px;
	cursor: pointer;
	 display: none;
	}

#skills{
	display: block;
	height: 1200px;
}
#skills h5{
	font-size: 30px;
	color: #212431;
	padding-bottom: 20px;
	padding-top: 20px;
	font-weight: bolder;
}
#skills h6{
	font-size: 20px;
	color: #212431;
	padding-bottom: 20px;
	padding-top: 20px;
	font-weight: bolder;
}
.personal{
	width: 50%;    
	padding-left: 0px;
	padding-bottom: 20px;
	color: white;
	font-size: 40px;
}
.Proffesional{
	width: 50%;
	padding-bottom: 20px;
	color: white;
	font-size: 40px;
}
 .personal h3{
	font-weight: 100;
	letter-spacing: 1px;
	margin-top: 20px;
	margin-bottom: 20px;
	color: black;
	font-size: 25px;
 }
 .Proffesional h3{
	font-weight: 100;
	letter-spacing: 1px;
	margin-top: 20px;
	margin-bottom: 20px;
	color: black;
	font-size: 25px;
 }
 .personal h5{
	margin-top: 10px;
	margin-bottom: 10px; 
	color: black;
 }
 .Proffesional h5{
	margin-top: 10px;
	margin-bottom: 10px;  
	color: black;
 }
 .progress_bar{
	width: 600px;
	height: 15px;
	border-radius: 5px;
	background-color: rgb(146, 146, 146);
 }
 .progress_bar .s1{
	height: 15px;
	border-radius: 5px;
	width: 30%;
	background-color: #212431;
 }
 .progress_bar .s2{
	height: 15px;
	border-radius: 5px;
	width: 70%;
	background-color: #212431;
 }
 .progress_bar .s3{
	height: 15px;
	border-radius: 5px;
	width: 90%;
	background-color: #212431;
 }
 .progress_bar .s4{
	height: 15px;
	border-radius: 5px;
	width: 60%;
	background-color: #212431;
 }
 .progress_bar .s5{
	height: 15px;
	border-radius: 5px;
	width: 60%;
	background-color: #212431
 }
 .progress_bar .s6{
	height: 15px;
	border-radius: 5px;
	width: 90%;
	background-color: #212431;
 }
 .progress_bar .s7{
	height: 15px;
	border-radius: 5px;
	width: 90%;
	background-color: #212431;
 }
 .progress_bar .s8{
	height: 15px;
	border-radius: 5px;
	width: 100%;
	background-color: #212431
 }
 .progress_bar div span{
	height: 40px;
	width: 40px;
	border-radius: 50%;
	background-color: rgb(215, 210, 150);
	float: right;
	margin-top: -15px;
	margin-right: 0px;
	color: black;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 15px;
	border: 1px lightgrey solid;
 } 

/* coloring nav, limiting the header,giving top border a line and a color */
/* header {
	width: 100%;
	height: 100px;
	background-color: rgba(145, 84, 224, 0.5);
} */
.whole-img {
	background-image: url(images/photo_2022-10-11_13-32-37.jpg);
	background-position: top;
	background-size: cover;
	background-repeat: no-repeat;
	background-attachment: fixed;
	/* background-color: #430e74;
		background-blend-mode: overlay;
		opacity: 0.8; */
}

/* nav bar objects to center by 80 % */
.primary-header {
	/* width: 100%;
	height: 100%;
	display: flex; */
	align-items: center;
	justify-content: space-between;
}

/* sending the logo to the left */
.logo {
	width: 20%;
	height: 120px;
	margin-left: 1px;
	padding-left: 0;
	float: left;
}

.logo img {
	width: auto;
	height: 100%;
	display: flex;
	float: left;
}

/* 2 slelectors adding rotation to the logo */
.logo img:hover {
	width: auto;
	height: 100%;
	display: flex;
	float: left;
	animation: rotation 5s infinite linear;
}

@keyframes rotation {
	from {
		transform: rotate(0deg);
	}

	to {
		transform: rotate(360deg);
	}
}

/* limiting the navigation to make it fit within 100% of the width */
nav {
	width: 100%;
	height: 100%;
	display: block;
	align-items: center;
	justify-content: space-between;
}

/* flex div used "new" */
.flex {
	display: flex;
	gap: var(--gap, 3rem)
}

.button-toggle {
	display: none;
}

/* spacing and adjusting the nav bar */
.primary-navigation {
	list-style: none;
	padding: 0;
	margin-top: 0;
	margin-right: 40px;
	float: right;
	justify-content: spaced-evenly;
	display: flex;
	background-color: hsl(0, 0%, 0%, .5);
}

/* removing the list buttons */
ul {}

/* modifying the list letters */
.primary-navigation {
	font-size: 21px;
	font-family: sans-serif;
	font-weight: normal;
	letter-spacing: 1px;
	color: #eee;
}

/* list or anchor hover adjustments */
.primary-navigation a:hover {
	font-size: 23px;
	transition: 0.2s all;
	font-family: sans-serif;
	font-weight: 700;
	letter-spacing: 1px;
}

/* working on a single word to make it a button */
.contactbtn {
	background-color: #eee;
	padding: 10px 20px;
	border-radius: 50px;
	font-weight: 700;
	color: #ff0505 !important;
}

/* button hover property */
.contactbtn:hover {
	background-color: #eee;
	padding: 10px 28px;
	transition: 0.2s all;
	border-radius: 50px;
	font-weight: 700;
	color: #ff0505 !important;
}

/* hero height,length and background */
.hero {
	width: 100%;
	height: 540px;
	max-height: 560px;
	margin-bottom: 50px;

	/* alternative : start */
	/* background-image: url(images/spiral.jpg);
	background-position: top;
	background-size: cover;
	background-color: #430e74;
	background-blend-mode: overlay;
	opacity: 0.8; */
	/* : end */
}

/* hero text div// limiting */
.herotext {
	width: 80%;
	height: auto;
	margin: auto;
}

/* adjusting the hero text properties */
/* fixed text */
/* .herotext h1 {
	width: 50%;
	margin-top: 10%;
	float: left;
	font-family: 'Courier New', Courier, monospace;
	font-size: 70px;
	text-align: right;
	color: #fff;
	font-weight: bolder;
	text-transform: uppercase;
	line-height: 90px;
	letter-spacing: 1px;
} */

/* sliding animation for the hero text */
.first-txt{
	width: 50%;
		margin-top: 5%;
		float: left;
		font-family: 'Courier New', Courier, monospace;
		font-size: 70px;
		text-align: right;
		color: #fff;
		font-weight: bolder;
		text-transform: uppercase;
		line-height: 90px;
		letter-spacing: 1px;
		animation: slide 5s ease-out;
}

@keyframes slide {
	0% {
		margin-left: -800px;
	}

	20% {
		margin-left: -800px;
	}

	35% {
		margin-left: 0px;
	}

	100% {
		margin-left: 0px;
	}
}

/* div of body */
.bodycontent {
	width: 80%;
	height: auto;
	margin: 0 auto 70px auto;
}

/* project title */
.projecth {
	width: 25%;
	margin: auto;
	padding-left: 200px;
	align-content: center;
	font-family: sans-serif;
	color: #21053b;
	margin-top: 30px;
	padding-bottom: 1rem;
}

/* body content padding and alignment */
.bodycontent {
	padding: 15px;
	margin-top: 16px;
	font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
	color: #111;
	font-weight: 400;
	text-align: center;
	line-height: 30px;
}

/* adjusting the body header */
h2.about {
	text-align: center;
	margin-top: 20px;
	font-family: sans-serif, 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS';
	font-size: 40px;
	padding-bottom: 15px;
	color: #21053b;
}

/* projects */
.projects {
	display: flex;
	justify-content: space-evenly;
	align-content: center;
	margin: 40px 0 30px 0;
}

/* centering the p in the body */
p {
	width 80%;
	padding-left: 10%;
	padding-right: 10%;
	font-family: cursive, sans-serif;
}

/* class of the first div in the projects/ project images */
.p1 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/Gen\ Z\ logo\ only.png);
	
	background-position: center;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

.p2 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/power.png);
	background-position: right;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

.p3 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/own.png);
	background-position: center;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

.p10 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc1.jpg);
	
	background-position: center;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

.p20 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc4.jpg);
	background-position: right;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

.p30 {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc3d.jpg);
	background-position: center;
	background-size: cover;
	box-shadow: 4px 4px 5px #a69b9b;
}

/* hover of the div in the projects/ project images */
.p1:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/Gen\ Z\ logo\ only.png);
	background-position: center;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

.p2:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/power.png);
	background-position: right;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

.p3:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(images/own.png);
	background-position: center;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

.p10:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc2.jpg);
	background-position: center;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

.p20:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc5.jpg);
	background-position: right;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

.p30:hover {
	width: 30%;
	height: 300px;
	position: relative;
	background-image: url(photo/arc9.jpg);
	background-position: center;
	background-size: cover;
	background-blend-mode: overlay;
	background-color: #430e74;
	transition: 0.4s all;
	transform: scale(1.07);
	box-shadow: 4px 4px 5px #a69b9b;
}

/* 
.root{
	primary:#fe58a0;
	text:#363636;
	light:#888888;
} */

/* projects=>p1,p2,p2=>plevel texts */
.plevel {
	width: 100%;
	height: 40%;
	position: absolute;
	top: 100%;
	font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
	font-size: 20px;
	font-weight: bold;
	color: #21053b;
	text-align: center;
	padding: 15px 0px 15px 0;
}

/* dash under the about class */
.line1 {
	width: 10%;
	height: 3px;
	margin-left: auto;
	margin-right: auto;
	background: #dd5242;
	margin-top: -3px;
}

/* dashes under the projects images */
.line2 {
	width: 10%;
	height: 3px;
	margin-left: auto;
	margin-right: auto;
	background: #dd5242;
	margin-top: -3px;
	position: relative;
	top: 120%;
}

/* dash for the project text */
.line3 {
	width: 10%;
	height: 3px;
	margin-left: auto;
	margin-right: auto;
	background: #dd5242
}

/* join me div */
.join {
	width: 100%;
	height: 300px;
	margin-top: 120px;
	padding-bottom: 30px;
	background: #21053b;
}

/* div containing question text, input and button */
.contactme {
	width: 80%;
	height: auto;
	margin: auto;
}

/* adjusting the question text */
.question {
	padding-top: 50px;
	text-align: center;
	font-size: 40px;
	font-family: sans-serif;
	font-weight: lighter;
	color: #999;
}

/* div of input and button adjustment of width and horizontal alignment */
.data {
	width: 70%;
	height: auto;
	margin: auto;
	display: flex;
	align-items: center;
}

/* adjusting the input width ,rad ,color and outline(border) */
.youremail {
	width: 65%;
	height: 50px;
	float: left;
	border-radius: 50px;
	margin-left: 3%;
	padding-left: 15px;
	border: 1px solid #ccc;
	outline: none;
}

/* placeholder color and size */
::placeholder {
	font-size: 18px;
	color: #999;
}

/* no space inorder to work */
/* inputed text */
input[type='email'] {
	font-size: 18px;
	color: #999
}

/* submit button rad, width, alignment and properties of text and object, border */
.button {
	width: 25%;
	height: 50px;
	float: left;
	margin-left: 2%;
	text-align: center;
	line-height: 50px;
	font-weight: 600;
	background: #dd5242;
	border: 0;
	border-radius: 50px;
	font-size: 20px;
	font-family: sans-serif;
}

.button:hover {
	width: 25%;
	height: 50px;
	transition: 0.2s all;
	transform: scale(1.1);
	float: left;
	margin-left: 2%;
	text-align: center;
	line-height: 50px;
	font-weight: 600;
	background: #090cbe;
	border: 0;
	border-radius: 50px;
	font-size: 20px;
	font-family: sans-serif;
}

/* footer div color,width, horizontal alignment , while keeping an even space between*/
footer {
	width: 100%;
	height: 70px;
	background-color: #000;
	display: flex;
	align-items: center;
	justify-content: space-between;
}

/* copyright text adjustment */
.copyright {
	font-weight: 400px;
	color: #7e7c7c;
	font-size: 14px;
	font-family: sans-serif;
	margin-left: 20px;
}

/* icons div size and also even space between*/
.socials {
	width: 10%;
	display: flex;
	justify-content: space-between;
	margin-right: 20px;
}

/* icons size adjustment */
.socials img {
	weight: 30px;
	height: 30px;
	transform: scale(1.0)
}

/* icons transformation when hovered on */
.socials img:hover {
	weight: 30px;
	height: 30px;
	cursor: pointer;
	transition: 0.4s all;
	transform: scale(1.3)
}

.git {
	padding-right: 20px;
}

/* mobile support */

/* a fall-back for browsers that doesn't support blur */
@supports (backdrop-filter: blur(.75rem)) {
	.primary-navigation {
		background-color: hsl(0, 0%, 100%, .2);
		backdrop-filter: blur(1rem);
	}
}

.primary-navigation a>[aria-hidden="true"] {
	font-weight: 700;
}

/* adjusting the sliding out menu (when visible) for the maximum possible screen */
/* 120% translateX is how far the menu goes off the screen */
@media (max-width: 35em) {
	.primary-navigation {
		position: absolute;
		height: 457px;
		z-index: 1000;
		--gap: 3rem;
		inset: 0 0 0 40%;
		flex-direction: column;
		padding: min(20vh, 10rem) 2rem;
		transform: translateX(120%);
		transition: transform 350ms ease-out;
	}
	.first-txt{
		margin-top: 1%;
	}

	/* for the min width- hidden menu */
	@media (min-width: 35em)
{
	/* active horizontal movement of the navigation elements while resizing the browser window */
		.primary-navigation {
			padding-block: 2rem;
			padding-inline: clamp(3rem, 5vw, 10rem);
		}
	}

	/* how much the menu pops out when clicked */
	.primary-navigation[data-visible="true"] {
		transform: translateX(16%);
	}

	/* importing and adjusting the button */
	.button-toggle {
		display: block;
		z-index: 9999;
		position: absolute;
		background-color: #999;
		background-image: url(images/3-dot.svg);
		width: 3rem;
		background-repeat: no-repeat;
		border: 0;
		aspect-ratio: 1;
		top: 2rem;
		right: 2rem;
		cursor: pointer;
	}

	/* button when expanded (x) */
	.button-toggle[aria-expanded="true"] {
		background-image: url(images/close.svg);
	}

	

/* expansion and contraction of the menu */
@media (min-width: 35em) and (max-width: 55em) {
	.primary-navigation a>[aria-hidden] {
		display: hidden;
	}
}

@media screen and (max-width: 35em) {
/* making the image fit the height of the screen */
	.whole-img {
		height: 700px;
	}

/* project text adjustment */
	.projecth {
		width: 25%;
		margin: auto;
		padding-left: 10px;
		align-content: center;
		font-family: sans-serif;
		color: #21053b;
		margin-top: 30px;
		padding-bottom: 1rem;
	}

	.logo img {
		width: auto;
		height: 100%;
		display: flex;
		float: left;
		animation: rotation 5s infinite linear;
	}
/* rotation of the logo when overed upon using the rotation/animation att. right on top of this code */
	@keyframes rotation {
		from {
			transform: rotate(0deg);
		}

		to {
			transform: rotate(360deg);
		}
	}

	/* adjusting the hero text to fit a smaller screen */
	.herotext h1 {
		width: auto;
		float: left;
		font-size: 50px;
		margin-top: 3rem;
	}

	/* adjusting the projects list to appear on top of eachother */
	.projects {
		flex-wrap: wrap;
	}

	.p1,
	.p2,
	.p3 {
		width: 100%;
		height: 300px;
		margin-bottom: 100px;
	}

	.p1:hover,
	.p2:hover,
	.p3:hover {
		width: 100%;
		height: 300px;
		margin-bottom: 30px;
		z-index: 500;
	}

	/* contact me section adjustment */
	.join {
		width: 100%;
		height: 400px;
	}

	.data {
		width: 100%;
	}

	.youremail {
		width: 100%;
		padding-left: 2rem;
	}

	::placeholder {
		font-size: 15px;
	}

	input [type='email'] {
		font-size: 15px;
	}

	.button {
		width: 70%;
		font-size: 18px;
	}

	.button:hover {
		width: 50%;
		font-size: 18px;
		transition: 0.4s all;
	}

	/* always apply the wrap attribute for the div element */

	/* aligning the footer elements to the center and above eachother */
	footer {
		flex-wrap: wrap;
	}

	.copyright {
		width: 100%;
		text-align: center;
	}

	.socials {
		width: 100%;
		margin-left: 50px;
		justify-content: center;
	}
}
    </style>
Add your Javascript sheets. You should create two JS sheets for your book one for the pages called
const primarynav = document.querySelector(".primary-navigation");
const navtoggle = document.querySelector(".button-toggle");

navtoggle.addEventListener('click', () => {
 const visibilty = primarynav.getAttribute('data-visible');

 if (visibilty === "false") {
  primarynav.setAttribute("data-visible", "true");
  navtoggle.setAttribute('aria-expanded', "true");
 }
 else if (visibilty === "true") {
  primarynav.setAttribute("data-visible", "false");
  navtoggle.setAttribute('aria-expanded', "false");
 }
})
