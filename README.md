# Assignment-2.4_Final-Project_Dhaval
Table PopulationData;
PFont labelFont;
PFont stateFont;

//Loading the Tables and the csv files
void setup() {
  size(850, 1050);
  labelFont = loadFont("Calibri-48.vlw");
  PopulationData = new Table();
  PopulationData = loadTable("india_pop.csv", "header");
  println(PopulationData.getRowCount() + " total rows in table");
}

void draw() {
  smooth();
  background(0);
  textFont(labelFont);
  strokeWeight(1);
  stroke(19, 116, 144);
  strokeWeight(3);
  fill(250);
  textAlign(LEFT);

//Drawing the rectangular bars of the x and y axis
  textAlign(CENTER);
  rectMode(CORNER);
  rect(0, 50, width, 10);
  rect(50, 0, 10, height);
  //line(0,50,width,50);
  //line(50,0,50,1000);
  
  
//drawing the ellipses that divide the rectangular bars
  strokeWeight(5);
  stroke(27, 91, 125, 100);
  for (int i = 150; i < 550; i+=100) {
    line(i, 50, i, 1000);
    ellipse(i, 55, 5, 5);
    fill(19, 116, 144);
    textSize(20);
    fill(250, 100);
    text(i/10, i, 40);
    textSize(20);
    



    //println(i);
  }
//drawing the ellipses that divide the rectangular bars vertically
  for (int b = 0; b<1050; b+=50) {
    ellipse(55, b, 5, 5);
    fill(250, 100);
    text(b-50, 25, b);
    textAlign(CENTER);
    textSize(20);
    fill(199, 228, 237, 10);
    text("DecadalGrowth v/s Density", 700, 40);
  }

  smooth();
  noStroke();

  for (TableRow row : PopulationData.rows ()) {

//drawing the ellipses that represent Decadal Growth, Population and Density

    int    density =   (row.getInt("7"));
    int    decaGrowth = ((row.getInt("8"))*10)+50;
    int    statePopulation = (row.getInt("3"))/1000000;

    fill(250, 240, 245, 160);
    ellipse(decaGrowth, density, statePopulation, statePopulation);
  }


//drawing the pink ellipses that represent number of males
  for (TableRow row : PopulationData.rows ()) {

    int    decaGrowth = ((row.getInt("8"))*10)+50;
    int    density =   (row.getInt("7"));
    int    stateMales = (row.getInt("4"))/1000000;
    fill(2, 112, 167, 100);
    stroke(200);
    strokeWeight(1);
    ellipse(decaGrowth, density, stateMales, stateMales);

    //fill(199,228,237,20);
    //text("DECADAL GROWTH v/s DENSITY", 600,40);
  }

  for (TableRow row : PopulationData.rows ()) {

    int    decaGrowth = ((row.getInt("8"))*10)+50;
    int    density =   (row.getInt("7"));
    int    stateMales = (row.getInt("4"))/1000000;
    String stateName  = row.getString("2");

//display text over the ellipses, such as the state names when mouse howers

    fill(250, 150);
    stroke(200);
    strokeWeight(1);
    textAlign(CENTER);


    if (dist(mouseX, mouseY, decaGrowth, density)<20) { 
      text(stateName, decaGrowth, density+15);
      textSize(15);
    }
  }
  for (TableRow row : PopulationData.rows ()) {

    int    stateSize  =  (row.getInt("9")/10000);
    int    decaGrowth = ((row.getInt("8"))*10)+50;
    int    density =   (row.getInt("7"));
    String stateName  = row.getString("2");
    String stateSimSize  = row.getString("10");
    String countryName  = row.getString("11");
    int    statePopulation = row.getInt("3");
    




//draw rectangles on the side, corresponding to the area and also display text below

    rectMode(CORNER);
    textAlign(LEFT);

    if (dist(mouseX, mouseY, decaGrowth, density)<20) { 
      fill(123, 56, 78, 160);
      stroke(250);
      strokeWeight(3);
      rect(525, 100, stateSize*5, stateSize*10);
      fill(250, 100);
      stateFont = loadFont("Ebrima-48.vlw");
      textFont(stateFont);
      textSize(18);
      text("Name of State - "+stateName, 525, (stateSize*10)+140);
      text("Population - "+ statePopulation, 525, (stateSize*10)+170);
      text("Area - " + stateSize*10000 + " sq.kms", 525, (stateSize*10)+200);
      text("Country of similar area - "+stateSimSize, 525, (stateSize*10)+230);
      text("Country of similar population - "+countryName, 525, (stateSize*10)+260);
      text("Density - " + density +" people/sq.km", 525, (stateSize*10)+290);
      text("Decadal Growth -  " + ((decaGrowth/10)-5)+ "%",525, (stateSize*10)+320);
    }
  }

}

  

