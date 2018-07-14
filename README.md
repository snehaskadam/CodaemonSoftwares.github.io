<html>
<head>
<style>
#listName{
   overflow-y:scroll;
   height:350px;
   display:block;
}
table {
    font-family: arial, sans-serif;
    width: 100%;
}

td,th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 5px;
	width:250px
}

tr:nth-child(even) {
    background-color: #dddddd;
}

</style>
<meta charset="utf-8">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.0/umd/popper.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.0/js/bootstrap.min.js"></script>
<script>

$(document).ready(function(){

	 $('#fname').click(function(){
	 document.getElementById("lastname").value="";
	 var fname = document.getElementById("firstname").value;
	 var urlFname = "https://data.cityofnewyork.us/resource/5scm-b38n.json?first_name=" + fname;
	 document.getElementById("listName").innerHTML='';
	 
	 $.getJSON(urlFname, function(result){
		document.getElementById("listprog").style.width = '100%'; 
        var htmlHdrText = '<table style="width:100%">';
		htmlHdrText += "<tr><th>Firstname</th><th>Lastname</th><th>Exam No</th><th>Agency</th><th>Title</th></tr>";
		$("#listName").append(htmlHdrText);
            $.each(result, function(i, field){	
				var htmlText = "";			
				htmlText += "<tr><td>" + field.first_name+"</td><td>"+field.last_name+"</td>";
				htmlText += "<td>" + field.exam_no+"</td><td>"+field.list_agency_desc+"</td>";
				htmlText += "<td>" + field.list_title_desc+"</td></tr>"
                htmlText += '</table>';				
				$("#listName").append(htmlText);
            });
        });		
		});
	
	$('#lname').click(function(){
	document.getElementById("firstname").value ="";
	var lname = document.getElementById("lastname").value;
	 var urlLname = "https://data.cityofnewyork.us/resource/5scm-b38n.json?last_name=" + lname;
	 document.getElementById("listName").innerHTML='';
	 
        $.getJSON(urlLname, function(result){			
			document.getElementById("listprog").style.width = '100%'; 
			var htmlHdrText = '<table style="width:100%">';
			htmlHdrText += "<tr><th>Firstname</th><th>Lastname</th><th>Exam No</th><th>Agency</th><th>Title</th></tr>";
			$("#listName").append(htmlHdrText);
			
            $.each(result, function(i, field){	
				var htmlText = "";
			    htmlText += "<tr><td>" + field.first_name+"</td><td>"+field.last_name+"</td>";
				htmlText += "<td>" + field.exam_no+"</td><td>"+field.list_agency_desc+"</td>";
				htmlText += "<td>" + field.list_title_desc+"</td></tr>"
                htmlText += '</table>';
				$("#listName").append(htmlText);
            });
        });
    });
		
	});
    
</script>
</head>
<body>
    <br>First name:<br>
		<input type="search" name="firstname" id="firstname" placeholder="Search Name.."><button id="fname">Search</button>
    <br>Last name:<br>
		<input type="search" name="lastname" id="lastname" placeholder="Search Last Name.."><button id="lname">Search</button>
    <br>
	<br>
	
 <div class="progress">
    <div id="listprog" class="progress-bar" style="width:0%;height:20%"></div>
  </div>
 
<div id="listName"></div>

</body>
</html>
