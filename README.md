<HTML>
<HEAD>
<TITLE>Right Triangle Trig Calculator</TITLE>


<SCRIPT language="JavaScript"><!--

function verify1()
{
        if (window.document.trigform.accuracy.selectedIndex == 0) { roundmultiplier = 1; }
   else if (window.document.trigform.accuracy.selectedIndex == 1) { roundmultiplier = 10; }
   else if (window.document.trigform.accuracy.selectedIndex == 2) { roundmultiplier = 100; }
   else if (window.document.trigform.accuracy.selectedIndex == 3) { roundmultiplier = 1000; }
   else if (window.document.trigform.accuracy.selectedIndex == 4) { roundmultiplier = 10000; }
   else if (window.document.trigform.accuracy.selectedIndex == 5) { roundmultiplier = 100000; }
   else if (window.document.trigform.accuracy.selectedIndex == 6) { roundmultiplier = 0; }

   sidea = window.document.trigform.sidea.value;
   sideb = window.document.trigform.sideb.value;
   sidec = window.document.trigform.sidec.value;
   anglx = window.document.trigform.anglx.value;

   sideaflag = "";
   sidebflag = "";
   sidecflag = "";
   anglxflag = "";
   filledflags = "";

   var emptyfield = 0;

   if ((sidea == "")||(sidea == " ")||(sidea == "  ")) { emptyfield = emptyfield + 1; } else { sideaflag = "a"; }
   if ((sideb == "")||(sideb == " ")||(sideb == "  ")) { emptyfield = emptyfield + 1; } else { sidebflag = "b"; }
   if ((sidec == "")||(sidec == " ")||(sidec == "  ")) { emptyfield = emptyfield + 1; } else { sidecflag = "c"; }
   if ((anglx == "")||(anglx == " ")||(anglx == "  ")) { emptyfield = emptyfield + 1; } else { anglxflag = "x"; }

   filledflags = sideaflag + sidebflag + sidecflag + anglxflag;

   if (emptyfield == 4) { alert("There are no fields filled. Pray tell, what would you have me calculate??") }
   if (emptyfield == 3) { alert("There is only one field filled. What do you expect me to calculate from that?") }
   if (emptyfield == 1) { alert("You have left only one field blank. I would rather you left two fields blank. Why? Because a third value is a derivative of the other two. I would have to assume that this third value is correct and I hate assuming things. If the third value is in error, it may throw my calculations off and I'd give you an incorrect answer. I definitely wouldn't want to do that.\n\nI suppose you might ask why don't I just check the given three values for errors? Well, the problem lies with accuracy. What if you give a value of 5 and the \"correct\" value is 4.998? That would flag as an error, but for most practical purposes it is not. I've therefore concluded that such error checking would cause more problems than it solves. So, we're back to asking for two values only.") }
   if (emptyfield == 0) { alert("You seem to have all fields filled out. What would you have me calculate? Leave two fields empty please.") }
   if (emptyfield == 2) { checkfornumber() }
}


function checkfornumber()
//kill if numbers are zero, negative or not numbers
{
   killprocess = 0;

   if (sideaflag == "a")
   {
           if (sidea == 0)         { alert("You've entered a value of zero for side A. Your triangle might now be a line."); killprocess = 1;}
      else if (sidea / sidea != 1) { alert("Side A does not appear to be a number. I can't do much with \"" + sidea + "\""); killprocess = 1; }
      else if (sidea < 0)          { alert("You've entered a negative value for side A. What's that all about?"); killprocess = 1; }
   }

   if ((sidebflag == "b")&&(killprocess == 0))
   {
           if (sideb == 0)         { alert("You've entered a value of zero for side B. Your triangle might now be a line."); killprocess = 1;}
      else if (sideb / sideb != 1) { alert("Side B does not appear to be a number. I can't do much with \"" + sideb + "\""); killprocess = 1; }
      else if (sideb < 0)          { alert("You've entered a negative value for side B. What's that all about?"); killprocess = 1; }
   }

   if ((sidecflag == "c")&&(killprocess == 0))
   {
           if (sidec == 0)         { alert("You've entered a value of zero for side C. Your triangle might now be a line."); killprocess = 1;}
      else if (sidec / sidec != 1) { alert("Side C does not appear to be a number. I can't do much with \"" + sidec + "\""); killprocess = 1; }
      else if (sidec < 0)          { alert("You've entered a negative value for side C. What's that all about?"); killprocess = 1; }
   }

   if ((anglxflag == "x")&&(killprocess == 0))
   {
           if (anglx == 0)         { alert("You've entered a value of zero for angle X. Your triangle might now be a line."); killprocess = 1;}
      else if (anglx / anglx != 1) { alert("Angle X does not appear to be a number. I can't do much with \"" + anglx + "\""); killprocess = 1; }
      else if (anglx < 0)          { alert("You've entered a negative value for angle X. What's that all about?"); killprocess = 1; }
      else if (anglx >= 90)        { alert("You've entered a value of 90 or greater for angle X. That kinda sorta makes it not a triangle."); killprocess = 1; }
   }

   if (killprocess == 0)
   {
      sidea = sidea * 1;
      sideb = sideb * 1;
      sidec = sidec * 1;
      anglx = anglx * 1;

      if (filledflags == "ab") { solve_ab(); }
      if (filledflags == "ac") { solve_ac(); }
      if (filledflags == "ax") { solve_ax(); }
      if (filledflags == "bc") { solve_bc(); }
      if (filledflags == "bx") { solve_bx(); }
      if (filledflags == "cx") { solve_cx(); }
   }
}




function solve_ab()
{
   // solve for side c
   sidec = (sidea * sidea) + (sideb * sideb);
   sidec = Math.sqrt(sidec);

   // solve for angle x
   tanx = sidea / sideb;
   atanx = Math.atan(tanx); // (result in radians)
   anglex = atanx * 180 / Math.PI; // converted to degrees

   // fill empty fields
   window.document.trigform.sidec.value = rounder(sidec);
   window.document.trigform.anglx.value = rounder(anglex);

   scaler();
}

function solve_ac()
{

   if (sidec > sidea)
   {
      // solve for side b
      sideb = (sidec * sidec) - (sidea * sidea);
      sideb = Math.sqrt(sideb);

      // solve for angle x
      tanx = sidea / sideb;
      atanx = Math.atan(tanx); // (result in radians)
      anglex = atanx * 180 / Math.PI; // converted to degrees

      // fill empty fields
      window.document.trigform.sideb.value = rounder(sideb);
      window.document.trigform.anglx.value = rounder(anglex);

      scaler();
   }
   else if (sidec == sidea)
   {
      alert("In a right triangle, side A cannot equal side C. You'll have to come up with different numbers.");
   }
   else if (sidec < sidea)
   {
      alert("In a right triangle, side A cannot be greater than side C. You'll have to come up with different numbers.");
   }
}

function solve_ax()
{
   // convert degrees to radians
   anglexinradians = anglx * Math.PI / 180

   // solve for side b
   sideb = sidea / Math.tan(anglexinradians);

   // solve for side c
   sidec = (sidea * sidea) + (sideb * sideb);
   sidec = Math.sqrt(sidec);
   
   // fill empty fields
   window.document.trigform.sideb.value = rounder(sideb);
   window.document.trigform.sidec.value = rounder(sidec);

   scaler();
}


function solve_bc()
{

   if (sidec > sideb)
   {
      // solve for side a
      sidea = (sidec * sidec) - (sideb * sideb);
      sidea = Math.sqrt(sidea);

      // solve for angle x
      tanx = sidea / sideb;
      atanx = Math.atan(tanx); // (result in radians)
      anglex = atanx * 180 / Math.PI; // converted to degrees

      // fill empty fields
      window.document.trigform.sidea.value = rounder(sidea);
      window.document.trigform.anglx.value = rounder(anglex);

      scaler();
   }
   else if (sidec == sideb)
   {
      alert("In a right triangle, side B cannot equal side C. You'll have to come up with different numbers.");
   }
   else if (sidec < sideb)
   {
      alert("In a right triangle, side B cannot be greater than side C. You'll have to come up with different numbers.");
   }
}


function solve_bx()
{
   // convert degrees to radians
   anglexinradians = anglx * Math.PI / 180

   // solve for side a
   sidea = Math.tan(anglexinradians) * sideb;

   // solve for side c
   sidec = (sidea * sidea) + (sideb * sideb);
   sidec = Math.sqrt(sidec);
   
   // fill empty fields
   window.document.trigform.sidea.value = rounder(sidea);
   window.document.trigform.sidec.value = rounder(sidec);

   scaler();
}


function solve_cx()
{
   // convert degrees to radians
   anglexinradians = anglx * Math.PI / 180

   // solve for side a
   sidea = Math.sin(anglexinradians) * sidec;

   // solve for side b
   sideb = Math.cos(anglexinradians) * sidec;
   
   // fill empty fields
   window.document.trigform.sidea.value = rounder(sidea);
   window.document.trigform.sideb.value = rounder(sideb);

   scaler();
}



function rounder(result)
{
   if (roundmultiplier == 0)
   {
      rounded = result;
      return rounded;
   }
   else
   {
      rounded = Math.round(result * roundmultiplier);
      rounded = rounded / roundmultiplier;
      return rounded;
   }
}


function scaler()
{
   if((sideb*1) >= (sidea*1))
   {
      imgwidth = 320;
      imgheight = Math.round(320 * sidea / sideb);
   }
   else
   {
      imgwidth = Math.round(320 * sideb / sidea);
      imgheight = 320;
   }

   if(top.floater)
   {
      top.floater.document.clear();
      top.floater.document.open();
      top.floater.document.write("<HTML><HEAD><TITLE></TITLE></HEAD><BODY STYLE=\"margin:1px\"><CENTER><IMG SRC=\"triangle.gif\" WIDTH=\"" + imgwidth + "\" HEIGHT=\"" + imgheight + "\" BORDER=\"0\"></CENTER></BODY></HTML>");
      top.floater.document.close();
   }
}


function clearfloater()
{
   if(top.floater)
   {
      top.floater.document.clear();
      top.floater.document.open();
      top.floater.document.write(" ");
      top.floater.document.close();
   }
}


function aboutwindow()
{
   aboutBox = window.open('about.html', 'About', 'width=400,height=320,resizable=yes');
}



//--></SCRIPT>


</HEAD>
<BODY>

<TABLE CELLSPACING="0" CELLPADDING="0" BORDER="0" ALIGN="center">

<TR>
<TD COLSPAN="2" ALIGN="center"><FONT SIZE="6" FACE="arial,helvetica">Right Triangle Trig Calculator<BR></FONT><FONT SIZE="2" FACE="arial,helvetica">Fill in two values and press Calculate. The other two values will be filled in.<BR>You may adjust the accuracy of your results.</FONT>
<NOSCRIPT><BR><FONT SIZE="2" FACE="arial,helvetica" COLOR="#FF0000"><B>Use of this page requires that Javascript be enabled. Yours seems to be disabled.</B></FONT></NOSCRIPT>
<HR SIZE="1"></TD>
</TR>

<TR>
<TD><IMG SRC="trig.gif" WIDTH="210" HEIGHT="150" BORDER="0" USEMAP="#aboutmap"></TD>
<TD>

<FONT FACE="courier new"><FORM NAME="trigform">
Side&nbsp;A&nbsp;=&nbsp;&nbsp;<INPUT TYPE="text" NAME="sidea" VALUE="" SIZE="24"><BR>
Side&nbsp;B&nbsp;=&nbsp;&nbsp;<INPUT TYPE="text" NAME="sideb" VALUE="" SIZE="24"><BR>
Side&nbsp;C&nbsp;=&nbsp;&nbsp;<INPUT TYPE="text" NAME="sidec" VALUE="" SIZE="24"><BR>
Angle&nbsp;X&nbsp;=&nbsp;<INPUT TYPE="text" NAME="anglx" VALUE="" SIZE="24">&nbsp;degrees<BR>
Accuracy&nbsp;=&nbsp;<SELECT NAME="accuracy">
<OPTION>nearest whole number - 1
<OPTION>tenths - .1
<OPTION SELECTED>hundredths - .01
<OPTION>thousandths - .001
<OPTION>10 thousandths - .0001
<OPTION>100 thousandths - .00001
<OPTION>no rounding
</SELECT><BR>
<INPUT TYPE="button" NAME="calc" VALUE="Calculate" onClick="verify1()">&nbsp;<INPUT TYPE="reset" NAME="calc" VALUE="Clear values" onClick="clearfloater();"><BR>
</FORM>
</FONT>
</TD>
</TR>

<TR>
<TD COLSPAN="2" ALIGN="center"><HR SIZE="1"><FONT SIZE="4" FACE="arial,helvetica">Triangle rendered to scale:</FONT></TD>
</TR>

</TABLE>

<IFRAME NAME="floater" width="324" height="324" SRC="float.html" ALIGN="center" FRAMEBORDER="no" SCROLLING="no">
<TABLE CELLSPACING="0" CELLPADDING="5" BORDER="0" WIDTH="452" ALIGN="center" BGCOLOR="#FFFFDD">
<TR><TD ALIGN="center"><FONT SIZE="1" FACE="verdana,arial,helvetica" COLOR="#EE2222">This page uses floating frames. If you were using a browser that "did" floating frames (such as Internet Explorer), you would be able to see a scaled triangle rendered here. But, since you're not, you don't ;-)</FONT></TD></TR>
</TABLE>
</IFRAME> 

<BR><IMG SRC="triangle.gif" HEIGHT="1" WIDTH="1" BORDER="0">
<IMG SRC="blank.gif" HEIGHT="1" WIDTH="1" BORDER="0">
<IMG SRC="icon.gif" WIDTH="1" HEIGHT="1" BORDER="0">

<MAP NAME="aboutmap">
<AREA SHAPE=RECT COORDS="0,138,28,150" HREF="javascript:aboutwindow()" onClick="aboutwindow();return false" ALT="About Right Triangle Trig Calculator">
</MAP>

</BODY>
</HTML>
