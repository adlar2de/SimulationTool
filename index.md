<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<meta http-equiv="X-UA-Compatible" content="ie=edge">

	<title>Rotodynamic Simulation Tool</title>

	<link rel="stylesheet" type="text/css" href="https://cdn.macodeid.com/maicons-v1.0/css/maicons.css">

	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">

	<link rel="stylesheet" href="../assets/vendor/animate/animate.css">

	<link rel="stylesheet" href="../assets/css/theme.css">
	<style>
		.popuptable{
			position:absolute;
			bottom:20vh;
			left:20vw;
			font-size: 18px;
			color:#1E1C1C;
			background-color:rgba(4,144,144,0.4);
			border-radius: 25px 25px 25px 25px;
			border: 5px solid rgba(38,60,60,0.8);
			padding: 5px;
			height:30vh;
			width:25vw;
			opacity:1;
			z-index:100;
		}
		.MyTables{
			border: 5px solid rgba(33,153,153,0.7);
			border-radius: 10px 10px 10px 10px;
			z-index:2;
			width:fit-content;
		}
		table{
		text-align:center;
		}
		th{
		border-collapse:collapse;
		border-radius:5px;
		text-align:center;
		}
		td{
		text-align:center;
		}
		.MyButton{
			color: #fff;
			background-color: #6C55F9;
			border-color: transparent;
			border-radius:5px;
		}
		select,input{
			color:#1E1C1C;
			background-color:rgba(4,144,144,0.4);
			text-align:center;
		}
		.pop-out{
			transition: transform .5s;
			z-index:2;
		}
		.pop-out:hover{
			z-index:10
			-ms-transform: scale(2,2);
			-webkit-transform: scale(2,2);
			transform: scale(2,2);
		}
	</style>
</head>
<body>

  <!-- Back to top button -->
  <div class="back-to-top"></div>

  <header>
    <nav class="navbar navbar-expand-lg navbar-light bg-white sticky" data-offset="500">
      <div class="container">
        <a href="#" class="navbar-brand">Aritz<span class="text-primary">Dorronsoro</span></a>

        <button class="navbar-toggler" data-toggle="collapse" data-target="#navbarContent" aria-controls="navbarContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="navbar-collapse collapse" id="navbarContent">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item active">
              <a class="nav-link" href="#Tutorial" data-role="smoothscroll">Tutorial</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#SimSetup" data-role="smoothscroll">Parameters</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#About" data-role="smoothscroll">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#Results" data-role="smoothscroll">Results</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#Contact" data-role="smoothscroll">Contact</a>
            </li>
            <li class="nav-item">
              <a class="btn btn-primary ml-lg-2" href="#" onclick=SimulationAlert()>Run Simulation</a>
            </li>
          </ul>
        </div>

      </div>
    </nav>

    <div class="container" id="Tutorial">
      <div class="page-banner home-banner">
        <div class="row align-items-center flex-wrap-reverse h-100">
          <div class="col-md-6 py-5 wow fadeInLeft">
            <h1 class="mb-4">Simulation Tool: Rotodynamic Analysis</h1>
            <p class="text-lg text-grey mb-5">(DEMO) Work in progress (DEMO)</p>
            <a href="#" class="btn btn-primary btn-split" onclick=PlayTutorial() id='PlayButton'> Watch Tutorial <div class="fab"><span class="mai-play"></span></div></a>
          </div>
          <div class="col-md-6 py-5 wow zoomIn">
            <div class="img-fluid text-center">
				<video width=400 controls id='TutorialVideo'>
					<source src="https://github.com/adlar2de/SimulationTool/blob/main/Files/PyFFTW_Trimmed_32.mp4?raw=true" type="video/mp4">
				</video>
            </div>
          </div>
        </div>
        <a href="#About" class="btn-scroll" data-role="smoothscroll"><span class="mai-arrow-down"></span></a>
      </div>
    </div>
  </header>

  <div class="page-section">
  <!-- POPUP TABLES -->
    <!-- TABLE 1: Geometry -->
	<div id="GeometryTable" title="Geometry" style="display:none" class=popuptable>
		<table style="width:100%; height:100%; background-color:rgba(4,144,144,0.7)">
			<tr>
				<th style="background-color:rgba(4,144,144,0.7)">L</th>
				<th style="background-color:rgba(4,144,144,0.7)">SPAN</th>
				<th style="background-color:rgba(4,144,144,0.7)">x<sub>1</sub></th>
				<th onclick=DisplayGeomTable() > <span class="mai-close-circle"></span> </th>
			</tr>
			<tr>
				<td contenteditable>100</td>
				<td contenteditable>80</td>
				<td contenteditable>10</td>
			</tr>
			<tr style="background-color:rgba(4,144,144,0.7)">
				<th>&#x2300 d</td>
				<th>&#x2300 D</td>
				<th>E</td>
			</tr>
			<tr>
				<td contenteditable>20</td>
				<td contenteditable>50</td>
				<td contenteditable>20</td>
			</tr>
			<tr style="background-color:rgba(4,144,144,0.7)">
				<th>x<sub>2</sub></td>
				<th>B</td>
				<th>B<sub>2</sub></td>
			</tr>
			<tr>
				<td contenteditable>40</td>
				<td contenteditable>5</td>
				<td contenteditable>5</td>
			</tr>
		</table>
	</div>
	<div style="position:absolute;display:none; bottom:20vh; left:50vw; z-index:100" id="GeomSketches">
		<img src="https://github.com/adlar2de/SimulationTool/blob/main/Files/Images/Sketch_Annotations.png?raw=true" alt="" height=300>
	</div>
	<!-- Geometry Table Finished  -->
	<!-- TABLE 2: Analysis -->
	<div id="AnalysisTable" title="Analysis" style="display:none" class=popuptable>
		<table style="width:100%; height:100%; background-color:rgba(4,144,144,0.7)">
			<tr>
				<th style="background-color:rgba(4,144,144,0.7)">&omega;<sub>MAX</sub> (RPM) </th>
				<th style="background-color:rgba(4,144,144,0.7)">N<sub>&omega;</sub></th>
				<th style="background-color:rgba(4,144,144,0.7)">N<sub>M</sub></th>
				<th onclick=DisplayAnalysisTable() > <span class="mai-close-circle"></span> </th>
			</tr>
			<tr>
				<td contenteditable>50 000</td>
				<td contenteditable><input type="number" value=10 min=1 style="width:8vh"></td>
				<td contenteditable><input type="number" value=10 min=1 style="width:8vh"></td>
			</tr>
		</table>
	</div>
	<div style="position:absolute;display:none; bottom:20vh; left:45vw; z-index:100" id="AnalysisSketches">
		<img src="https://github.com/adlar2de/SimulationTool/blob/main/Files/Images/Campbell_Annotated.png?raw=true" alt="" height=350>
	</div>
	<!-- Analysis Table Finished -->
	<!-- TABLE 3: Advanced -->
	<div id="AdvancedTable" title="Advanced" style="display:none" class=popuptable>
		<table style="width:100%; height:100%; background-color:rgba(4,144,144,0.7)">
			<tr>
				<th style="background-color:rgba(4,144,144,0.7)">Mesh</th>
				<th style="background-color:rgba(4,144,144,0.7)">N<sub>CPU</sub></th>
				<th onclick=DisplayAdvancedTable() > <span class="mai-close-circle"></span> </th>
			</tr>
			<tr>
				<td class="select" >
					<select>
						<option value="Extra Coarse">Extra Coarse</option>
						<option value="Coarse">Coarse</option>
						<option value="Fine">Fine</option>
						<option value="Extra Fine">Extra Fine</option>
					</select>
				</td>
				<td contenteditable><input type="number" value=1 min=1 style="width:10vh"></input></td>
			</tr>
		</table>
	</div>
	<div style="position:absolute;display:none; bottom:20vh; left:45vw; z-index:100" id="Mesh">
		<img src="https://github.com/adlar2de/SimulationTool/blob/main/Files/Images/Mesh.png?raw=true" alt="" height=350>
	</div>
	<!-- Analysis Table Finished -->
	<!-- END POPUP TABLES -->
    <div class="container" id="SimSetup">
	  <span class="subhead">Parameters</span>
      <div class="row">
        <div class="col-lg-4">
          <div class="card-service wow fadeInUp">
            <div class="header">
              <img src="../assets/img/services/service-1.svg" alt="">
            </div>
            <div class="body">
              <h5 class="text-secondary">Geometry</h5>
              <p>Define geometry of the system</p>
			  <p>All measures are in mm</p>
				<button onclick=DisplayGeomTable() id='GeometryButton' class=tablebutton> Set Geometry </button>
            </div>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="card-service wow fadeInUp">
            <div class="header">
              <img src="../assets/img/services/service-2.svg" alt="">
            </div>
            <div class="body">
              <h5 class="text-secondary">Analysis</h5>
              <p>Decide important parameters for the simulations</p>
			  <button onclick=DisplayAnalysisTable() id='AnalysisButton' class=tablebutton> Analysis Parameters </button>
            </div>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="card-service wow fadeInUp">
            <div class="header">
              <img src="../assets/img/services/service-3.svg" alt="">
            </div>
            <div class="body">
              <h5 class="text-secondary">Advanced</h5>
              <p>Only for experienced users</p>
			  <button onclick=DisplayAdvancedTable() id='AdvancedButton' class=tablebutton> Advanced Parameters </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="page-section" id="About">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-lg-6 py-3 wow fadeInUp">
          <span class="subhead">About the tool</span>
          <h2 class="title-section">Reliable mechanical solver: ABAQUS</h2>
          <div class="divider"></div>
			<p>Normal modes and natural frequencies of the rotating system are calculated using the finite element based solver ABAQUS.</p>
          <a href="https://www.3ds.com/products-services/simulia/products/abaqus/" target="_blank" class="btn btn-primary mt-3">Read More</a>
        </div>
        <div class="col-lg-6 py-3 wow fadeInRight">
          <div class="img-fluid py-3 text-center">
			<img src="https://github.com/adlar2de/SimulationTool/blob/main/Files/Images/Simulation_Default.png?raw=true" alt="" width=400>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="page-section" id="Results">
    <div class="container-fluid">
      <div class="text-center wow fadeInUp">
        <div class="subhead">Results</div>
        <h2 class="title-section">Visualise Vibration Modes</h2>
        <div class="divider mx-auto"></div>
      </div>
      <div class="row mt-5">
        <div class="col-lg-4 py-3 wow zoomIn" >
          <div class="card-pricing" id="TableCol">
            <div class="header">
              <div class="pricing-type">Table</div>
              <div class="price">
                <h1>Frequency Values<span class="suffix">(Hz)</span></h1>
              </div>
            </div>
            <div class="body">
			<center>
			  <table id="CampbellTable" class=MyTables>
			  </table>
			</center>
            </div>
            <div class="footer">
			  <button onclick="LoadCampbell()" class="MyButton" id="TableButton"> Load </button>
            </div>
          </div>
        </div>

        <div class="col-lg-4 py-3 wow zoomIn" >
          <div class="card-pricing marked" id="SecondCol">
            <div class="header">
              <div class="pricing-type">Graphic</div>
              <div class="price">
                <h1>Campbell Diagram</h1>
              </div>
            </div>
            <div class="body">
              <img src="../assets/img/Campbell_Default.png" width=100% class="pop-out" id="DefaultCampbell"> </img>
            </div>
          </div>
        </div>

        <div class="col-lg-4 py-3 wow zoomIn">
          <div class="card-pricing" id="ThirdCol">
            <div class="header">
              <div class="pricing-type">Geometry</div>
              <div class="price">
                <h1>ABAQUS Geometry</h1>
              </div>
            </div>
            <div class="body">
              <img src="https://github.com/adlar2de/SimulationTool/blob/main/Files/Images/Sim_1.png?raw=true" width=100% id="AbqGeom"> </img>
            </div>
            <div class="footer">
              <button onclick="ChangeGeom()" class="MyButton" id="GeomButton"> Next </button>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <div class="page-section banner-info">
    <div class="wrap bg-image" style="background-image: url(../assets/img/bg_pattern.svg);">
      <div class="container">
        <div class="row align-items-center">
          <div class="col-lg-6 py-3 pr-lg-5 wow fadeInUp">
            <h2 class="title-section">Missing Features</h2>
            <div class="divider"></div>
            <p>This page is only a demo. There are two main features that will be added in the future:</p>
            
            <ul class="theme-list theme-list-light text-white">
              <li>
                <div class="h5">Actual Simulation Capabilities</div>
                <p>All the data and figures have been pre-simulated. No actual simulation is happening.<br>Acces to a server with ABAQUS software (and available runtime licenses) is necessary for this.</p>
              </li>
              <li>
                <div class="h5">Serious Visualisation Tool</div>
                <p>Result visualisation options are limited at the moment: a table with the relevant data, a figure showing a Campbell Diagram, and images of the normal modes.<br>Comparison between different normal modes and simultaneous visualisation of various modes/views will be possible in future versions.</p>
              </li>
            </ul>
          </div>
          <div class="col-lg-6 py-3 wow fadeInRight">
            <div class="img-fluid text-center">
              <img src="../assets/img/banner_image_2.svg" alt="">
			  <p> This image will be substituted by a more relevant one, too. </p>
            </div>
          </div>
        </div>
      </div>
    </div> 
  </div> 

  <footer class="page-footer bg-image" style="background-image: url(../assets/img/world_pattern.svg);" id="Contact">
    <div class="container-fluid">
      <div class="row mb-5">
        <div class="col-lg-4 py-4">
          <h3>Aritz Dorronsoro</h3>
          <p>PhD Student in CEIT.</p>
		  <p> Socials (below) still not working.</p>

          <div class="social-media-button">
            <a href="#Contact"><span class="mai-logo-facebook-f"></span></a>
            <a href="#Contact"><span class="mai-logo-twitter"></span></a>
            <a href="#Contact"><span class="mai-logo-google-plus-g"></span></a>
            <a href="#Contact"><span class="mai-logo-instagram"></span></a>
            <a href="#Contact"><span class="mai-logo-youtube"></span></a>
          </div>
        </div>
        <div class="col-lg-4 py-4">
          <h5>CV (Pending)</h5>
          <ul class="footer-menu">
            <li><a href="#Contact">About Me</a></li>
            <li><a href="#Contact">Contact</a></li>
          </ul>
        </div>
        <div class="col-lg-4 py-4">
          <h5>Contact Me</h5>
          <p>Manuel Lardizabal ibilbidea 15<br>
		  20018 Donostia, Gipuzkoa</p>
		  <p>(+34) 943 212 800<br>Ext. 2118</p>
          <p>adlarbide@ceit.es</p>
        </div>
      </div>

      <p class="text-center" id="copyright">Copyright &copy; 2020. This webpage is an adaptation of a template by <a href="https://macodeid.com/projects/seogram-free-seo-agency-template/" target="_blank">MACode ID</a></p>
    </div>
  </footer>

<script src="../assets/js/jquery-3.5.1.min.js"></script>

<script src="../assets/js/bootstrap.bundle.min.js"></script>

<script src="../assets/js/google-maps.js"></script>

<script src="../assets/vendor/wow/wow.min.js"></script>

<script src="../assets/js/theme.js"></script>

<script>
	var im = document.getElementById('DefaultCampbell')
	im.addEventListener('mouseover',MouseOver);
	im.addEventListener('mouseout',MouseOut);
	function MouseOver(e){
		document.getElementById('TableCol').style.display = 'none'
		document.getElementById('ThirdCol').style.display = 'none'
	}
	function MouseOut(e){
		document.getElementById('TableCol').style.display = 'block'
		document.getElementById('ThirdCol').style.display = 'block'
	}
	function PlayTutorial(){
		var tv = document.getElementById('TutorialVideo')
		tv.currentTime = 0.;
		tv.play();
	}
	function DisplayGeomTable(){
		TableStyle = document.getElementById("GeometryTable").style
		TableStyle.height = 140
		TableStyle.modal = true
		if (TableStyle.display == 'block'){
			TableStyle.display = 'none'
			document.getElementById("GeomSketches").style.display = 'none'
			document.getElementById('SimSetup').style.filter = 'none';
			document.getElementById('GeometryButton').disabled = false;
			document.getElementById("AnalysisButton").disabled = false;
			document.getElementById("AdvancedButton").disabled = false;
		} else {
			document.getElementById("GeomSketches").style.display = 'block'
			TableStyle.display = 'block'
			document.getElementById('SimSetup').style.filter = "blur(3px)";
			document.getElementById('GeometryButton').disabled = true;
			document.getElementById("AnalysisButton").disabled = true;
			document.getElementById("AdvancedButton").disabled = true;
		}
	};
	function DisplayAnalysisTable(){
		TableStyle = document.getElementById("AnalysisTable").style
		TableStyle.height = 140
		TableStyle.modal = true
		if (TableStyle.display == 'block'){
			TableStyle.display = 'none'
			document.getElementById("AnalysisSketches").style.display = 'none'
			document.getElementById('SimSetup').style.filter = 'none';
			document.getElementById('GeometryButton').disabled = false;
			document.getElementById("AnalysisButton").disabled = false;
			document.getElementById("AdvancedButton").disabled = false;
		} else {
			TableStyle.display = 'block'
			document.getElementById("AnalysisSketches").style.display = 'block'
			document.getElementById('SimSetup').style.filter = "blur(3px)";
			document.getElementById('GeometryButton').disabled = true;
			document.getElementById("AnalysisButton").disabled = true;
			document.getElementById("AdvancedButton").disabled = true;
		}
	};
	function DisplayAdvancedTable(){
		TableStyle = document.getElementById("AdvancedTable").style
		TableStyle.height = 140
		TableStyle.modal = true
		if (TableStyle.display == 'block'){
			TableStyle.display = 'none'
			document.getElementById("Mesh").style.display = 'none'
			document.getElementById('SimSetup').style.filter = 'none';
			document.getElementById('GeometryButton').disabled = false;
			document.getElementById("AnalysisButton").disabled = false;
			document.getElementById("AdvancedButton").disabled = false;
		} else {
			TableStyle.display = 'block'
			document.getElementById("Mesh").style.display = 'block'
			document.getElementById('SimSetup').style.filter = "blur(3px)";
			document.getElementById('GeometryButton').disabled = true;
			document.getElementById("AnalysisButton").disabled = true;
			document.getElementById("AdvancedButton").disabled = true;
		}
	}	;
	function CreateMatrix(nx,ny){
		<!-- console.log(nx,ny) -->
		var Out = []
		for (var i=0; i<nx; i++){
			Out[i] = [];
			for (var j=0; j<ny; j++){
				Out[i][j] = undefined;
			}
		}
		return Out
	}
	function TransposeMatrix(M){
		Transposed = M[0].map((_, colIndex) => M.map(row => row[colIndex]))
		return Transposed
	}
	async function LoadCampbell(){
		T = document.getElementById("CampbellTable")
		if (T.rows.length==0){
			mytxt = await ReadTextFromGitHub()
			Rows = mytxt.split('\n')
			NRow = Rows.length - 1 
			NCols = Rows[0].split(',').length
			DataMatrix = CreateMatrix(NRow,NCols)
			T = document.getElementById("CampbellTable")
			for (var i=0 ; i<NRow ; i++){
				txtRow = Rows[i].split(',');
				for (var j=0 ; j<NCols ; j++){
					DataMatrix[i][j] = txtRow[j];
				}
			}
			DataMatrix = TransposeMatrix(DataMatrix);
			for (var i=0 ; i<NCols ; i++){
				Row = T.insertRow()
				for (var j=0 ; j<NRow ; j++){
					Cell = Row.insertCell()
					Cell.innerHTML = DataMatrix[i][j]
					Cell.style.backgroundColor = "rgba(4,144,144,0.4)"
					Cell.style.borderLeft = "2px solid black"
				}
				Row.cells[0].style.borderLeft=""
				Row.cells[0].style.backgroundColor="rgba(4,144,144,0.6)"
			}
			T.rows[0].style.borderBottom="2px solid black"
			T.rows[0].style.backgroundColor="rgba(4,144,144,0.6)"
		}
		if(T.style.display=="none" || T.style.display==""){
			document.getElementById("TableButton").innerHTML = "Hide"
			T.style.display = "block"
			document.getElementById("SecondCol").style.display="none"
			document.getElementById("ThirdCol").style.display="none"
		}else{
			document.getElementById("TableButton").innerHTML = "Load"
			T.style.display = "none"
			document.getElementById("SecondCol").style.display="block"
			document.getElementById("ThirdCol").style.display="block"
		}
		<!-- console.log(DataMatrix) -->
		<!-- return DataMatrix -->
	}
	async function ReadTextFromGitHub(){
		const url = 'https://raw.githubusercontent.com/adlar2de/SimulationTool/main/Files/CampbellData.csv'
		const response = await fetch(url);
		const data = await response.text();
		return data
	}
	async function ChangeGeom(){
		urlName = document.getElementById("AbqGeom").src
		urlCutoff = urlName.length-14
		n = Number(urlName[urlCutoff])
		newN = n+1
		if(newN==9){newN=1}
		newUrl = urlName.substring(0,urlCutoff) + newN + urlName.substring(urlCutoff+1)
		document.getElementById("AbqGeom").src = newUrl
	}
	function SimulationAlert(){
		alert("Still not functional...")
	}
</script>
  
</body>
</html>
