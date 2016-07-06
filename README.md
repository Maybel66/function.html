# function.html
<html>
<head>

	<script
				  src="http://code.jquery.com/jquery-3.0.0.min.js"
				  integrity="sha256-JmvOoLtYsmqlsWxa7mDSLMwa6dZ9rrIdtrrVYRnDRH0="
				  crossorigin="anonymous"></script>
	<link rel="stylesheet" type="text/css" href="function.css">
<!--<link href="src/theme/default.css" rel="stylesheet">-->


    </head>
<body>
	<img id="imgZoom" width="200px" height="180px" onmousemove="zoomIn(event)" onmouseout="zoomOut()" src="images/Proteins/Keratin.jpg">
<div id="overlay" onmousemove="zoomIn(event)"></div>
  <!--<img onmouseover="bigImg(this)" onmouseout="normalImg(this)" border="0" src="images/Proteins/Keratin.jpg" alt="Smiley" width="200" height="180" >-->

<!--<img id="myimg" src="images/Proteins/Keratin.jpg" width ="200" height= "180">-->

<div class="images"></div>

  <script type="text/javascript">
  cars = [
    {
      name: "Albumin",
      location: [380, 3, 5],
      distance: 20,
     src:"images/Proteins/Albumin.jpg",
		 title: "The name of this protein is",
     description: "Albumin"


},
    {
      name: "Tubulin",
      location: [180,20, 40],
        distance: 9,
        src:"images/Proteins/Tubulin.jpg",
				title: "This is a text",
description:"Tubulin"

    },
    {
      name: "Myosin",
      location: [40, 60, 70],
        distance: 5,
        src:"images/Proteins/Myosin.jpg",
description:"Myosin"

    },
    {
      name: "Collagen",
      location: [200,10, 60],
        distance: 12,
        src:"images/Proteins/Collagen.jpg",
description:"Collagen"
    }
  ]

	function zoomIn(event) {
	  var element = document.getElementById("overlay");
	  element.style.display = "inline-block";
	  var img = document.getElementById("imgZoom");
	  var posX = event.offsetX ? (event.offsetX) : event.pageX - img.offsetLeft;
	  var posY = event.offsetY ? (event.offsetY) : event.pageY - img.offsetTop;
	  element.style.backgroundPosition = (-posX * 4) + "px " + (-posY * 4) + "px";

	}

	function zoomOut() {
	  var element = document.getElementById("overlay");
	  element.style.display = "none";
	}

var oImg = '';
	$.each(cars, function(key, val) {
	          oImg = '<div class="images"><img src="' + val.src + '" class="img-thumbnail thumb m-r" width="100" height="100"/><span>' + val.description + '</span></div>';

	          $(".images").append(oImg);
	});



    $(document).on("click", ".pics", function(e){

          var id = $(this).data("id");
           console.log(id);



          //console.log(cars[id].distance);
         cars = recalculate_distance(cars, id);
          cars.sort (function(a, b){return a.distance -b.distance;})
          $(".images").html("");
        var i =0;
      for(i=0; i<cars.length; i++){

          var oImg = document.createElement("IMG");
          oImg.setAttribute('src', cars[i].src);
          oImg.setAttribute('alt', 'na');
          oImg.setAttribute('height', '100px');
          oImg.setAttribute('width', '100px');
          oImg.setAttribute('index', i);
          oImg.setAttribute('class', 'pics');
          oImg.setAttribute('data-id', i);
    oImg.setAttribute('title', cars[i].title);

          $(".images").append(oImg);

      }
		})



    var i =0;
      for(i=0; i<cars.length; i++){
          var oImg = document.createElement("IMG");
          oImg.setAttribute('src', cars[i].src);
          oImg.setAttribute('alt', 'na');
          oImg.setAttribute('height', '100px');
          oImg.setAttribute('width', '100px');
          oImg.setAttribute('index', i);
          oImg.setAttribute('class', 'pics');
          oImg.setAttribute('data-id', i);
          oImg.setAttribute('title', cars[i].title);


         $(".images").append(oImg);
      }
function recalculate_distance(cars, anchorIndex) {
    var i =0;
  for (i=0; i<cars.length; i++)
  {
    cars[i].distance = Euclidean_distance (cars[i].location, cars[anchorIndex].location)
    console.log(cars[i].distance);
  }
  return cars                // The function returns the product of p1 and p2
}
function Euclidean_distance(pt1, pt2) {
	var d= 0;
	for (i =0; i<pt1.length; i++)
	{
		d = d + (pt1[i]-pt2[i])*(pt1[i]-pt2[i]);
	}
	return Math.sqrt(d);
}
  </script>
</body>
</html>
