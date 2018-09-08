<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml" lang="pt-br" xml:lang="pt-br">
 <meta http-equiv="content-type" content="application/xhtml+xml; charset=utf-8" />
</meta>

<?xml version="1.0" encoding="UTF-8" standalone="no" ?>

    <head>
        <title>Demonstração de curvas cardióides</title>
	    <script src="https://d3js.org/d3.v5.min.js"></script>
    </head>
    <style>
		th, td {
		    text-align: left;
		    
		}
	</style>

    <body>

        <p>Implementação de curvas cardióides em SVG. Como desenhar essas curvas <a href="https://ferramentasexcelvba.wordpress.com/2018/09/02/mil-cardioides-no-excel/">aqui</a> </p>
	
	<table style = "width:30%">
  	<tr>
    <th>Pontos:</th>
    <th>Step:</th>
    </tr>
    <tr>
    <td>
    <form>
		  <select onchange = "Desenha()" name="Pontos" id="SelectPontos">
		    <option value="5">5</option>
		    <option value="10">10</option>
		    <option value="15">15</option>
		    <option value="20">20</option>
		    <option value="30">30</option>
		    <option value="50">50</option>
		    <option value="100" selected>100</option>
		    <option value="200">200</option>
		    <option value="500">500</option>
		  </select>
		  <br><br>
		</form>
		</td>
    
    <td>	   <form>
		  <select onchange = "Desenha()" name="Step" id="SelectStep">
		    <option value="0">0</option>
		    <option value="1">1</option>
		    <option value="2" selected>2</option>
		    <option value="3">3</option>
		    <option value="4">4</option>
		    <option value="5">5</option>
		    <option value="6">6</option>
		  </select>
		  <br><br>
		</form>
	</td>
	  </tr>
	</table>
	       
       
	

	
        <script type = "text/javascript">


        var svg = d3.select("body").append("svg");


        var limX = 700;
        var limY = 500;
        
        //Define dimensions of svg
        svg.attr("width", limX)
        .attr("height",limY);

        Desenha();

        

         


        function Desenha()
        {
        	//alert (d3.select("#SelectPontos").property("value"));
        
        //Clear svg
		svg.selectAll("*").remove();

        //dados e definicoes macro
        var raio = (limY - 100)/2;
        var N = d3.select("#SelectPontos").property("value");
        var step =d3.select("#SelectStep").property("value");
        var corR = Math.floor(Math.random() * 200) ;
        var corG = Math.floor(Math.random() * 200) ;
        var corB = Math.floor(Math.random() * 2mnkl00) ;

        //Traça o círculo inicial
        var circle0 = svg.selectAll("circle")
        	.data([1])
        	.enter()
        	.append("circle");

        var cx0 = 100+(limX -raio)/2;
        var cy0 = 51+(limY-raio)/2;

        circle0.attr("cx", cx0)
        		.attr("cy", cy0)
        		.attr("r", raio)
        		.attr("fill", "white")
        		.attr("stroke","rgb(" + corR + "," + corG + "," + corB + ")")
        		.attr("stroke-width","1")
        		;

        //Traça os círculos menores
        var i;
        var cx1 =[];
        var cy1 =[];
        var theta;

        //consertar o array 0
        //Cria o array de dados
        for (i = 0; i<= N; i++)
        {	
        	theta = 2*Math.PI*i/N;
        	cx1.push(cx0 + raio*Math.cos(theta));
        	cy1.push(cy0 + raio*Math.sin(theta));
        }

        //Cria os pontos
        var circle1 = svg.selectAll("circle")
        	.data(cx1)
        	.enter()
        	.append("circle");

        circle1.attr("cx", function(d,i){
        			return cx1[i];
        		})
        		.attr("cy", function(d,i){
        			return cy1[i];
        		})
        		.attr("r", 2)
        		.attr("fill", "rgb(" + corR + "," + corG + "," + corB + ")")
        		.attr("stroke","rgb(" + corR + "," + corG + "," + corB + ")")
        		.attr("stroke-width","1")
        		;

        //Cria as linhas
        var px0 =[];
        var py0 =[];
        var px1 =[];
        var py1 =[];
        var j;

        for(i =0; i<N; i++)
        {
        	
	        j = (i*step + (parseInt(N)  + parseInt(N % 2)) / 2 ) % N;

        	px0.push(cx1[i]);
        	py0.push(cy1[i]);
        	px1.push(cx1[j]);
        	py1.push(cy1[j]);
        }

        //Desenha as linhas
        var lines = svg.selectAll("line")
        	.data(px0)
        	.enter()
        	.append("line");

        lines.attr("x1", function(d,i){
        			return px0[i];
        		})
        		.attr("y1", function(d,i){
        			return py0[i];
        		})
        		.attr("x2", function(d,i){
        			return px1[i];
        		})
        		.attr("y2", function(d,i){
        			return py1[i];
        		})
        		.attr("stroke","rgb(" + corR + "," + corG + "," + corB + ")")
        		.attr("stroke-width","1")
        		;
        	}	
		</script>

    </body>
</html>
