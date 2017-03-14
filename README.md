# Nonijus
<script>
/*var soundID = "Thunder";

 function loadSound () {
        createjs.Sound.registerSound("assets/thunder.ogg", soundID);
      }

      function playSound () {
        createjs.Sound.play(soundID);
      }*/
//Runge- Kuta metod za diferencijalne jednačine drugog reda
function Runge(f,g,z0,w0,t0,t,h){
var wi = w0;//console.log('n',(t - t0)/h)
var zi = z0;
var n = (t - t0)/h;
for(var i = 0;i < n;i++){
var t = t0 + h*i;
var k1 = h*f(t,wi,zi);
var l1 = h*g(t,wi,zi);
var k2 = h*f((t + h/2),(wi + k1/2),(zi + l1/2));
var l2 = h*g((t + h/2),(wi + k1/2),(zi + l1/2));
var k3 = h*f((t + h/2),(wi + k2/2),(zi + l2/2));
var l3 = h*g((t + h/2),(wi + k2/2),(zi + l2/2));
var k4 = h*f((t + h),(wi + k3),(zi + l3));
var l4 = h*g((t + h),(wi + k3),(zi + l3));
wi += (k1 + 2*k2 + 2*k3 + k4)/6;
zi += (l1 + 2*l2 + 2*l3 + l4)/6;
//console.log('i',i,'l1',k1,'l2',k2,'l3',l3,'k4',l4,'wi',wi,'zi',zi)
//console.log('i',i,'k1',k1,'k2',k2,'k3',k3,'k4',k4,'wi',wi,'zi',zi)
};
return wi;
}//Kraj Runge
//funkcija za prvi izvod
var c0 = Math.PI*14/180;
var k = 1;
//var c1 = 90000/64/6.4;
function g(x,y,z){
return (k/(1 - Math.cos(y)) - 48.5*(y - c0) - 3.2*z);
}
//Bazna funkcija
function f(x,y,z){
return z;
}

//Direktiva za selekciju elemenata
app.directive('svgInternal', function () {
var telo = '<g id="telo" ng-mousedown="elementMouseDown($event)" '+
'ng-mouseleave= "mouseLeave()" ng-mouseenter="mouseEnter()"' +
'ng-attr-transform=" translate({{element.x}},{{element.y}})'+
'rotate({{element.rotation.degree}}, {{element.rotation.x}}, {{element.rotation.y}})">' +
'<g  ng-show="isSelected" ng-attr-transform=" translate({{-element.x}},{{-element.y}})">'+
            '<circle class="NS" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[4].x}}" ng-attr-cy="{{elementSelections[4].y}}" r="4" />'+
            '<circle class="EW" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[5].x}}" ng-attr-cy="{{elementSelections[5].y}}" r="4" />'+
            '<circle class="NS" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[6].x}}" ng-attr-cy="{{elementSelections[6].y}}" r="4" />'+
            '<circle class="EW" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[7].x}}" ng-attr-cy="{{elementSelections[7].y}}" r="4" />'+
            '</g>' +
            '<g  ng-show="isSelected" ng-attr-transform=" translate({{-element.x}},{{-element.y}})">'+
            '<circle class="rotacija" id="rotir" fill="#00F000" stroke-width="2" ng-attr-cx="{{elementSelections[8].x}}" ng-attr-cy="{{elementSelections[8].y}}" r="4" />'+
            '<line ng-attr-x1="{{elementSelections[5].x}}" ng-attr-y1="{{elementSelections[5].y}}" ng-attr-x2="{{elementSelections[8].x}}" ng-attr-y2="{{elementSelections[5].y}}" style="stroke:rgb(0,0,0);stroke-width:1" />'+
            '</g>' +
'<g  ng-show="isSelected" ng-attr-transform=" translate({{-element.x}},{{-element.y}})">'+
       '<circle id="dl" class="dijag" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[0].x}}" ng-attr-cy="{{elementSelections[0].y}}" r="4" />'+
       '<circle id="gl" class="dijag" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[1].x}}" ng-attr-cy="{{elementSelections[1].y}}" r="4" />'+
       '<circle id="gd" class="dijag" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[2].x}}" ng-attr-cy="{{elementSelections[2].y}}" r="4" />'+
       '<circle id="dd" class="dijag" fill="#3003DC" stroke-width="2" ng-attr-cx="{{elementSelections[3].x}}" ng-attr-cy="{{elementSelections[3].y}}" r="4" />'+
            '</g></g>';
     function link(scope,element,attr){
     angular.element("#rotir").mousedown(function(event){
     scope.isRotacija = true;
            var selekcija = event.target;
            scope.selektElement = selekcija;
     //Priprema za rotaciju, obeležavanje elementa       
          });
    //Inicijacija razvlaćenja  
        angular.element(".dijag").mousedown(function(event){
     scope.isDdijag = true;
     });
    
       };
     
    return {
      templateNamespace: 'svg',
      template: telo,
      restrict: 'E',
      replace: true,
      link: link
    };
  });

app.directive('valjak', function() {
    function link(element,attr){
if(attr.x0==null){attr.x0 = 100;};
if(attr.y0==null){attr.y0 = 100;};
if(attr.opacityBaze==null){attr.opacityBaze = 1;};
if(attr.opacityOmotaca==null){attr.opacityOmotaca = 1;};
if(attr.sirinaLinijeBaze==null){attr.sirinaLinijeBaze = 1;};
if(attr.sirinaLinije==null){attr.sirinaLinije = 1;};
if(attr.bojaBaze==null){attr.bojaBaze = "yellow";};
if(attr.bojaOmotaca==null){attr.bojaOmotaca = "green";};
if(attr.bojaLinije==null){attr.bojaLinije = "blue";};
 var telo = Telo(attr.class,attr.x0*1,attr.y0*1,attr.theta0*1,attr.theta*1,
 attr.phi*1,attr.r*1,attr.h*1,attr.bojaBaze,attr.bojaOmotaca,
 attr.bojaLinije,attr.opacityBaze,attr.opacityOmotaca,attr.sirinaLinije,attr.sirinaLinijeBaze);
 return telo;
  };
  
    return {
      templateNamespace: 'svg',
      restrict: 'E',
      replace: true,
      template:link
      
    };
})
//Zarubljena kupa
app.directive('zKupa', function() {
    function link(element,attr){
if(attr.x0==null){attr.x0 = 100;};
if(attr.y0==null){attr.y0 = 100;};
if(attr.opacityBaze==null){attr.opacityBaze = 1;};
if(attr.opacityOmotaca==null){attr.opacityOmotaca = 1;};
if(attr.sirinaLinijeBaze==null){attr.sirinaLinijeBaze = 1;};
if(attr.sirinaLinije==null){attr.sirinaLinije = 1;};
if(attr.bojaBaze==null){attr.bojaBaze = "yellow";};
if(attr.bojaOmotaca==null){attr.bojaOmotaca = "green";};
if(attr.bojaLinije==null){attr.bojaLinije = "blue";};
 var telo = Teloz(attr.x0*1,attr.y0*1,attr.theta0*1,attr.theta*1,
 attr.phi*1,attr.r1*1,attr.r2*1,attr.h*1,attr.bojaBaze,attr.bojaOmotaca,
 attr.bojaLinije,attr.opacityBaze,attr.opacityOmotaca,attr.sirinaLinije,attr.sirinaLinijeBaze);
 return telo;
  };
  
    return {
      templateNamespace: 'svg',
      restrict: 'E',
      replace: true,
      template:link
      
    };
})

//Pozivna funkcija za valjak
function Telo(clasa,x0,y0,theta0,theta,phi,R,H,bojaBaze,bojaOmotaca,
bojaLinije,opacityBaze,opacityOmotaca,sirinaLinije,sirinaLinijeBaze){
var theta = Math.PI/180*theta;
var theta0 = Math.PI/180*theta0;
var phi = Math.PI/180*phi;
//console.log(opacityBaze,opacityOmotaca,sirinaLinije);
var alp0 = Math.atan((Math.cos(theta)*Math.sin(theta0) - 
Math.sin(theta)*Math.sin(phi)*Math.cos(theta0))/
Math.sin(theta)/Math.cos(phi));

var x1 = x0 -R*Math.sin(alp0)*Math.sin(phi) + 
R*Math.cos(alp0)*Math.cos(phi)*Math.cos(theta0);
var y1 = y0 + R*Math.cos(alp0)*Math.sin(theta)*Math.sin(theta0) +
R*Math.cos(phi)*Math.cos(theta)*Math.sin(alp0) +
R*Math.cos(theta)*Math.sin(phi)*Math.cos(theta0)*Math.cos(alp0);
var xk = x0 +R*Math.sin(alp0)*Math.sin(phi) - 
R*Math.cos(alp0)*Math.cos(phi)*Math.cos(theta0);
var yk = y0 - R*Math.cos(alp0)*Math.sin(theta)*Math.sin(theta0) -
R*Math.cos(phi)*Math.cos(theta)*Math.sin(alp0) -
R*Math.cos(theta)*Math.sin(phi)*Math.cos(theta0)*Math.cos(alp0);
var a0 = Math.sin(theta0)*Math.sin(theta) +
Math.cos(theta0)*Math.cos(theta)*Math.sin(phi);
var delta = Math.cos(theta0)*Math.cos(theta) +
Math.sin(theta0)*Math.sin(theta)*Math.sin(phi);
if(theta == Math.PI/2 && theta0 == Math.PI/2 &&
phi == 0){
var a = 0;
var b = R;
var c = 0;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var obrt = 0;
var telo = '<g>';
telo += '<path class="'+clasa+'" d="M'+ x1 +' '+ y1 +'  a'+ a +','+ b +' 0 1,1 0,'+2*b+'';
telo += 'l '+d+' -'+c+' a'+ a +','+ b +' 0 0,0 0,-'+2*b+'';
telo += 'l -'+d+' '+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else if(theta0 == Math.PI/2 && theta == 0){
var a = 0;
var b = R;
var c = 0;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var obrt = 0;
var telo = '<g>';
telo += '<path class="'+clasa+'" d="M'+ x1 +' '+ y1 +'  a'+ a +','+ b +' 0 1,1 0,'+2*b+'';
telo += 'l '+d+' -'+c+' a'+ a +','+ b +' 0 0,0 0,-'+2*b+'';
telo += 'l -'+d+' '+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else{
var A = (a0*a0 + Math.cos(theta)*Math.cos(theta)*Math.cos(phi)*Math.cos(phi))
/(delta*delta*R*R);
var B = (Math.cos(phi)*Math.cos(phi)*Math.cos(theta0)*Math.cos(theta0) + 
Math.sin(phi)*Math.sin(phi))/(delta*delta*R*R);
var C = 2*(a0*Math.cos(theta0)*Math.cos(phi) - 
Math.sin(phi)*Math.cos(theta)*Math.cos(phi))/(delta*delta*R*R);
if(B == A){
if(C > 0){
var alpha = Math.PI/4 }else{var alpha =-Math.PI/4};
if(C==0){var alpha = 0};
}else{
var alpha = 1/2*Math.atan(C/(B - A));
}
var aInv = A*Math.cos(alpha)*Math.cos(alpha) +
B*Math.sin(alpha)*Math.sin(alpha) -
C*Math.sin(alpha)*Math.cos(alpha);
var bInv = B*Math.cos(alpha)*Math.cos(alpha) +
A*Math.sin(alpha)*Math.sin(alpha) +
C*Math.sin(alpha)*Math.cos(alpha);
var a = 1/Math.sqrt(aInv);
var b = 1/Math.sqrt(bInv);
var obrt = 180*alpha/Math.PI;
var c = -H*(Math.cos(theta0)*Math.sin(theta) - 
Math.cos(theta)*Math.sin(theta0)*Math.sin(phi));
var d = H*Math.sin(theta0)*Math.cos(phi);
if(Math.sin(2*phi) > 0){
var f1 = 1;
var f2 = 0;
}else{
var f1 = 0;
var f2 = 1;
};
if(Math.sin(phi) > 0){
var x1k = x1 + d;
var y1k = y1 + c;
var telo = '<g>';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a+'" ry="'+b+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'" '+
' transform="rotate('+obrt+' '+x0+' '+ y0+')"/>';
telo += '<path class="'+clasa+'" d="M'+ x1 +' '+ y1 +'  A'+ a +','+ b +' '+obrt+' 0,'+f1+' '+xk+','+yk+'';
telo += 'l '+(d)+' '+(c)+' A'+ a +','+ b +' '+obrt+' 0,'+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d)+' '+(-c)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="two" cx="'+x0+'" cy="'+y0+'" rx="'+a+'" ry="'+b+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+';" '+
' transform="rotate('+obrt+' '+(x0+d)+' '+(y0+c)+') translate('+d+','+c+')"/></g>';

}else{
var x1k = x1 + d;
var y1k = y1 + c;
var telo = '<g>';
telo += '<ellipse id="two" cx="'+x0+'" cy="'+y0+'" rx="'+a+'" ry="'+b+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+';" '+
' transform="rotate('+obrt+' '+(x0+d)+' '+(y0+c)+') translate('+d+','+c+')"/>';

telo += '<path class="'+clasa+'" d="M'+ x1 +' '+ y1 +'  A'+ a +','+ b +' '+obrt+' 0,'+f1+' '+xk+','+yk+'';
telo += 'l '+(d)+' '+(c)+' A'+ a +','+ b +' '+obrt+' 0,'+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d)+' '+(-c)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a+'" ry="'+b+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'" '+
' transform="rotate('+obrt+' '+x0+' '+ y0+')"/></g>';
};

};

return telo;
}//Kraj funkcije Telo valjka
//Pozivna funkcija za zarubljenu kupu
function Teloz(x0,y0,theta0,theta,phi,R1,R2,H,bojaBaze,bojaOmotaca,
bojaLinije,opacityBaze,opacityOmotaca,sirinaLinije,sirinaLinijeBaze){

var theta = Math.PI/180*theta;
var theta0 = Math.PI/180*theta0;
var phi = Math.PI*phi/180;
var r = R1*1 - R2*1;
var hi = Math.atan(r/H);
var a0 = Math.sin(theta0)*Math.sin(theta) +
Math.cos(theta0)*Math.cos(theta)*Math.sin(phi);
var delta = Math.cos(theta0)*Math.cos(theta) +
Math.sin(theta0)*Math.sin(theta)*Math.sin(phi);
var a = a0*a0 + Math.cos(theta)*Math.cos(theta)*Math.cos(phi)*Math.cos(phi);
var b = Math.cos(phi)*Math.cos(phi)*Math.cos(theta0)*Math.cos(theta0) + 
Math.sin(phi)*Math.sin(phi);
var c = 2*(a0*Math.cos(theta0)*Math.cos(phi) - 
Math.sin(phi)*Math.cos(theta)*Math.cos(phi));
var d0 = H*Math.sin(theta0)*Math.cos(phi);
var c0 = H*(Math.cos(theta0)*Math.sin(theta) - 
Math.cos(theta)*Math.sin(theta0)*Math.sin(phi));
var D = (a*b-c*c/4)*(c0*c0*b + d0*d0*a  + c0*d0*c - r*r*delta*delta);
var k =((d0*c0*(a*b-c*c/4) + c*r*r*delta*delta/2) + delta*r*Math.sqrt(D))/
(-delta*delta*r*r*b + (a*b-c*c/4)*d0*d0);
//console.log('k',k);
var alpha = 1/2*Math.atan(c/(b - a));
if(b == a){
if(c > 0){
var alpha = Math.PI/4 }else{var alpha =-Math.PI/4};
if(c == 0){var alpha = 0};
}else{
var alpha = 1/2*Math.atan(c/(b - a));
}
var aInv = a*Math.cos(alpha)*Math.cos(alpha) +
b*Math.sin(alpha)*Math.sin(alpha) -
c*Math.sin(alpha)*Math.cos(alpha);
var bInv = b*Math.cos(alpha)*Math.cos(alpha) +
a*Math.sin(alpha)*Math.sin(alpha) +
c*Math.sin(alpha)*Math.cos(alpha);
var del = Math.abs(delta);
var a1 = R1*del/Math.sqrt(aInv);
var b1 = R1*del/Math.sqrt(bInv);
var a2 = R2*del/Math.sqrt(aInv);
var b2 =  R2*del/Math.sqrt(bInv);
var obrt = 180*alpha/Math.PI;

if(Math.sin(2*phi) > 0){
var f1 = 1;var i1 = 1;
var f2 = 0;var i2 = 0;
}else{
var f1 = 1;var i1 = 1;
var f2 = 0;var i2 = 1;
};

if(theta == Math.PI/2 && theta0 == Math.PI/2 &&
phi == 0){
var a = 0;
var b = R1;
var c = R1 - R2;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var obrt = 0;
var telo = '<g>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  a'+ a +','+ b +' 0 1,1 0,'+2*b+'';
telo += 'l '+d+' -'+c+' a'+ a +','+ R2 +' 0 0,0 0,-'+2*R2+'';
telo += 'l -'+d+' -'+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else if(theta0 == Math.PI/2  && Math.abs(Math.sin(theta)) < 0.00001){
var a = 0;
var b = R1;
var c = R1 - R2;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var obrt = 0;
var telo = '<g>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  a'+ a +','+ b +' 0 1,1 0,'+2*b+'';
telo += 'l '+d+' -'+c+' a'+ a +','+ R2 +' 0 0,0 0,-'+2*R2+'';
telo += 'l -'+d+' -'+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else if(theta0 == Math.PI && theta == Math.PI/2){
var obrt = 0;
var a1 = R1*del/Math.sqrt(bInv);
var b1 = R1;
var a2 = R2*del/Math.sqrt(bInv);
var b2 =  R2;
var c = R1 - R2;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var telo = '<g>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  a'+ a1 +','+ b1 +' 0 1,1 '+2*a1+',0';
telo += 'l -'+d+' '+c+' a'+ R2 +',0 0 0,0 -'+2*R2+',0';
telo += 'l -'+d+' -'+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else if(theta0 == Math.PI/2 && (phi == 0 || phi == Math.PI)){
if(phi == 0){var obrt = 0;}else{var obrt = 180;}
var a = 0;
var b = R1;
var c = R1 - R2;
var d = H;
var x1 = x0 - a;
var y1 = y0 - b;
var telo = '<g>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  a'+ a +','+ b +' 0 1,1 0,'+2*b+'';
telo += 'l '+d+' -'+c+' a'+ R2 +',0 0 0,0 0,-'+2*R2+'';
telo += 'l -'+d+' -'+c+'"  transform="rotate('+obrt+' '+x0+' '+(y0)+')"';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/></g>';
}else{
if(D > 0 ){//console.log('D > 0');
var k1 = ((d0*c0*(a*b-c*c/4) + c*r*r*delta*delta/2) + delta*r*Math.sqrt(D))/
(-delta*delta*r*r*b + (a*b-c*c/4)*d0*d0);
var n1 = R1*(c0 - d0*k1)/r;
var xpr = -(b*k1 + c/2)*n1/(a + b*k1*k1 + c*k1);
var ypr = (a +c*k1/2)*n1/(a + b*k1*k1 + c*k1);
var x1 = x0 + xpr;
var y1 = y0 - ypr;
var k2 = ((d0*c0*(a*b-c*c/4) + c*r*r*delta*delta/2) - delta*r*Math.sqrt(D))/
(-delta*delta*r*r*b + (a*b-c*c/4)*d0*d0);
var n2 = R1*(c0 - d0*k2)/r;
var xpr = -(b*k2 + c/2)*n2/(a + b*k2*k2 + c*k2);
var ypr = (a +c*k2/2)*n2/(a + b*k2*k2 + c*k2);
var xk = x0 + xpr;
var yk = y0 - ypr;
var d1 = (b*k1*c0 + a*d0 +k1*c*d0/2 + c*c0/2)/(a + b*k1*k1 + c*k1);
var x1k = x1 + d1;;
var c1 = d1*k1;
var y1k = y1 - c1 ;
var d2 = (b*k2*c0 + a*d0 +k2*c*d0/2 + c*c0/2)/(a + b*k2*k2 + c*k2);
var c2 = d2*k2;
//console.log('c0',c0,'y1k',y1k,'x1k',x1k);
if(Math.sin(phi) >= 0){
var telo = '<g >';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a1+'" ry="'+b1+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'"'+
'transform="rotate('+(obrt)+' '+(x0)+' '+(y0)+')" />';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  A'+ a1 +','+ b1 +' '+(obrt)+' '+i1+','+f1+' '+xk+','+yk+'';
telo += 'l '+(d2)+' '+(-c2)+' A'+ a2 +','+ b2 +' '+(obrt)+' '+i2+','+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d1)+' '+(c1)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="two" cx="'+(x0+d0)+'" cy="'+(y0-c0)+'" rx="'+a2+'" ry="'+b2+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+'" '+
'transform="rotate('+(obrt)+' '+(x0+d0)+' '+(y0-c0)+') " />';
' </g >';
}else{
var f1 = 0;var i1 = 0;
var f2 = 0;var i2 = 0;
if(theta > Math.PI/2){
var f1 = 0;var i1 = 0;
var f2 = 1;var i2 = 0;
};

var telo = '<g>';
telo += '<ellipse id="two" cx="'+x0+'" cy="'+y0+'" rx="'+a2+'" ry="'+b2+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+';" '+
' transform="rotate('+obrt+' '+(x0+d0)+' '+(y0-c0)+') translate('+d0+','+(-c0)+')"/>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  A'+ a1 +','+ b1 +' '+(obrt)+' '+i1+','+f1+' '+xk+','+yk+'';
telo += 'l '+(d2)+' '+(-c2)+' A'+ a2 +','+ b2 +' '+(obrt)+' '+i2+','+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d1)+' '+(c1)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a1+'" ry="'+b1+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'" '+
' transform="rotate('+obrt+' '+x0+' '+ y0+')"/></g>';
};

}else{//D < 0
var f1 = 0;var i1 = 1;
var f2 = 1;var i2 = 1;
if(theta > Math.PI/2){
var f1 = 1;var i1 = 1;
var f2 = 0;var i2 = 1;
};
if(theta0 == Math.PI  ){
var f1 = 0;var i1 = 1;
var f2 = 1;var i2 = 1;
};
var x1 = x0 + R1*Math.sin(phi);
xk = x1 + R1*Math.cos(theta0)*Math.cos(phi)*0.001 ;
var y1 = y0 - R1*Math.cos(theta)*Math.cos(phi);
var yk = y1 + R1*0.001*(Math.cos(theta0)*Math.cos(theta)*Math.sin(phi) +
Math.sin(theta)*Math.sin(theta0));
x1k = x0 + d0 + R2*Math.sin(phi);
y1k = y0 - c0 - R2*Math.cos(theta)*Math.cos(phi);

var d1 = r*Math.sin(phi) - d0 ;
var c1 =r*Math.cos(theta)*Math.cos(phi) - c0; 

var telo = '<g >';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a1+'" ry="'+b1+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'"'+
'transform="rotate('+(obrt)+' '+(x0)+' '+(y0)+')" />';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  A'+ a1 +','+ b1 +' '+(obrt)+' '+i1+','+f1+' '+xk+','+yk+'';
telo += 'l '+(-d1)+' '+(c1)+' A'+ a2 +','+ b2 +' '+(obrt)+' '+i2+','+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(d1)+' '+(-c1)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="two" cx="'+(x0+d0)+'" cy="'+(y0-c0)+'" rx="'+a2+'" ry="'+b2+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+'" '+
'transform="rotate('+(obrt)+' '+(x0+d0)+' '+(y0-c0)+') " />';
' </g >';
if(Math.sin(phi) < 0){
var telo = '<g>';
telo += '<ellipse id="two" cx="'+x0+'" cy="'+y0+'" rx="'+a2+'" ry="'+b2+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+';" '+
' transform="rotate('+obrt+' '+(x0+d0)+' '+(y0-c0)+') translate('+d0+','+(-c0)+')"/>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  A'+ a1 +','+ b1 +' '+(obrt)+' '+i1+','+f1+' '+xk+','+yk+'';
telo += 'l '+(d2)+' '+(-c2)+' A'+ a2 +','+ b2 +' '+(obrt)+' '+i2+','+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d1)+' '+(c1)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a1+'" ry="'+b1+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'" '+
' transform="rotate('+obrt+' '+x0+' '+ y0+')"/></g>';
};
};
if(theta0 == Math.PI && Math.sin(theta) > 0){
var f1 = 0;var i1 = 0;
var f2 = 0;var i2 = 0;
var telo = '<g>';
telo += '<ellipse id="two" cx="'+x0+'" cy="'+y0+'" rx="'+a2+'" ry="'+b2+'"'
+ 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+';stroke-width:'+
sirinaLinijeBaze+';opacity: '+opacityBaze+';" '+
' transform="rotate('+obrt+' '+(x0+d0)+' '+(y0-c0)+') translate('+d0+','+(-c0)+')"/>';
telo += '<path class="nStap" d="M'+ x1 +' '+ y1 +'  A'+ a1 +','+ b1 +' '+(obrt)+' '+i1+','+f1+' '+xk+','+yk+'';
telo += 'l '+(d2)+' '+(-c2)+' A'+ a2 +','+ b2 +' '+(obrt)+' '+i2+','+f2+' '+(x1k)+','+y1k+'';
telo += 'l '+(-d1)+' '+(c1)+'" ';
telo +=  'style="stroke: '+bojaLinije+'; stroke-width:'+
sirinaLinije+';opacity: '+opacityOmotaca+'; fill:'+bojaOmotaca+';"/>';
telo += '<ellipse id="one" cx="'+x0+'" cy="'+y0+'" rx="'+a1+'" ry="'+b1+'"';
telo += 'style="fill:'+bojaBaze+';stroke:'+bojaLinije+
';opacity: '+opacityBaze+';stroke-width:'+sirinaLinijeBaze+'" '+
' transform="rotate('+obrt+' '+x0+' '+ y0+')"/></g>';
};

};
//console.log('zarubljena kupa',a1,a2,b1,b2);
return telo;
}//Kraj zarubljene kupe
  
 function SVG(tag)
{
   return document.createElementNS('http://www.w3.org/2000/svg', tag);
}



</script>

<script>
window.addEventListener('load', function() {
 var list = $('#dobrodoslica');
  list.empty();
  $('#dobrodoslica').text("Tестови из физике");
});

//Nonijus
 app.directive('nonijus', function($compile,$interval) {
 
   function link(element,attr){
   console.log('pre',element);
  //Definisanje strukture elementa
  var Telo = Nonijus(attr.x0*1,attr.y0*1,attr.sirina*1,attr.visina*1);console.log
  return Telo;
    };
    function povezi(scope,element,attr){
 
   element.on("dodir",function(event,log,q1,q2){
   
 
 });// Kraj mouse on
element.mousedown(function(event){
$(".pokaz").remove();
var selekcija = $(event.target)
if(selekcija.attr("class") == 'slider'){
scope.klizanje = true;isDragging = false;
}   
});
element.mouseup(function(event){
var l = scope.pomak/scope.nonijus.width/.004;
  var l0 = Math.floor(l);
  var i  = l0 + 50*(l - l0); var j = 50*(l - l0);
  var x1 = scope.nonijus.H.x + i*scope.nonijus.width*.004 + scope.nonijus.width*.016;
  var y1 = scope.nonijus.H.y;
  var y2 = scope.nonijus.H.y - scope.nonijus.height*0.067;
 // var x2 = scope.nonijus.H.x + scope.nonijus.width*.004*(l0 + j*49/50) + scope.nonijus.width*.016 ;
  var y3 = scope.nonijus.H.y + scope.nonijus.height*0.067;
  var line = SVG('line');
  $(line).attr("x1",x1).attr("x2",x1).attr("y1",y1).attr("y2",y2).
  attr("stroke",'red').attr("stroke.width",1).attr("class",'pokaz');
  element.append(line);
  var line = SVG('line');
  $(line).attr("x1",x1).attr("x2",x1).attr("y1",y1).attr("y2",y3).
  attr("stroke",'red').attr("stroke.width",1).attr("class",'pokaz');
  element.append(line);
  
});
   element.mousemove(function(event){

     });//Kraj mousemove
    
element.on("pokazi",function(){
scope.nonijus.A.x = scope.nonijus.x;scope.nonijus.A.y = scope.nonijus.y;
scope.nonijus.B.x = scope.nonijus.A.x - scope.nonijus.width*0.05;
scope.nonijus.B.y = scope.nonijus.A.y;
scope.nonijus.C.x = scope.nonijus.B.x ;
scope.nonijus.C.y = scope.nonijus.B.y + scope.nonijus.height*0.29;
scope.nonijus.D.x = scope.nonijus.C.x + scope.nonijus.width*0.023;
scope.nonijus.D.y = scope.nonijus.C.y + scope.nonijus.height*0.4;
scope.nonijus.E.x = scope.nonijus.D.x + scope.nonijus.width*0.023;
scope.nonijus.E.y = scope.nonijus.D.y;
scope.nonijus.F.x = scope.nonijus.E.x;
scope.nonijus.F.y = scope.nonijus.E.y - scope.nonijus.height*0.24;
scope.nonijus.G.x = scope.nonijus.F.x - scope.nonijus.width*0.005;
scope.nonijus.G.y = scope.nonijus.F.y;
scope.nonijus.H.x = scope.nonijus.G.x ;
scope.nonijus.H.y = scope.nonijus.G.y - scope.nonijus.height*0.16;
scope.nonijus.I.x = scope.nonijus.H.x + scope.nonijus.width*0.8;
scope.nonijus.I.y = scope.nonijus.H.y ;
scope.nonijus.J.x = scope.nonijus.I.x ;
scope.nonijus.J.y = scope.nonijus.I.y - scope.nonijus.height*0.2;
scope.nonijus.K.x = scope.nonijus.H.x + scope.nonijus.width*0.0085;
scope.nonijus.K.y = scope.nonijus.J.y ;
scope.nonijus.L.x = scope.nonijus.E.x ;
scope.nonijus.L.y = scope.nonijus.E.y + scope.nonijus.height*0.12;
scope.nonijus.M.x = scope.nonijus.A.x - scope.nonijus.width*0.02;
scope.nonijus.M.y = scope.nonijus.A.y - scope.nonijus.height*0.2;
scope.nonijus.N.x = scope.nonijus.L.x + scope.pomak;
scope.nonijus.N.y = scope.nonijus.L.y ;
 }); //Kraj pokazi  
    };//Kraj povezi
    return {
      templateNamespace: 'svg',
      restrict: 'E',
      replace: true,
      template: link,
      link:povezi,
      
      //transclude:true,
      
    };
});   



function Nonijus(x0,y0,sirina,visina) {
var telo = '<g   ng-show="nonijus.jeKreiran" ng-mousedown="elementMouseDown($event)" '+
'ng-mouseleave= "mouseLeave()" ng-mouseenter="mouseEnter()"' +
'ng-attr-transform="'+
'rotate({{nonijus.rotation.degree}}, {{nonijus.rotation.x}}, {{nonijus.rotation.y}})">' +
'<rect class="slider" ng-attr-x="{{nonijus.A.x + pomak + nonijus.width*0.005}}" ng-attr-y="{{nonijus.A.y}}"'+
'ng-attr-width="{{nonijus.width*0.216}}" ng-attr-height="{{nonijus.height*.087}}" '+
'style="fill:#a3a3c2;stroke-width:1;stroke:#a3a3c2" />'+
'<path class="slider" ng-attr-d="M {{nonijus.K.x + pomak + nonijus.width*0.005}} {{nonijus.K.y}} '+
'l{{-nonijus.width*.05}},0 l0,{{-nonijus.height*.087}} '+
  'A{{nonijus.width*.05}},{{nonijus.width*.1}} 0 0,1 {{nonijus.M.x + pomak}},{{nonijus.M.y}} l0,{{nonijus.height*0.16}}'+
  'l{{-nonijus.width*.002}},0 l0,{{nonijus.height*0.04}} l{{nonijus.width*.026}},0 z"'+
  ' stroke="#a3a3c2" stroke-width="1" fill="#a3a3c2" />'+
' <polyline ng-attr-points="{{nonijus.A.x}},{{nonijus.A.y}}'+
' {{nonijus.B.x}},{{nonijus.B.y}} {{nonijus.C.x}},{{nonijus.C.y}} '+
' {{nonijus.D.x}},{{nonijus.D.y}} {{nonijus.E.x}},{{nonijus.E.y}}'+
' {{nonijus.F.x}},{{nonijus.F.y}} {{nonijus.G.x}},{{nonijus.G.y}}'+
' {{nonijus.H.x}},{{nonijus.H.y}} {{nonijus.I.x}},{{nonijus.I.y}}'+
' {{nonijus.J.x}},{{nonijus.J.y}} {{nonijus.K.x}},{{nonijus.K.y}} {{nonijus.A.x}},{{nonijus.A.y}}"'+
  'style="fill:#a3a3c2;stroke:#a3a3c2;stroke-width:1" />' +
 '<path  ng-attr-d="M {{nonijus.D.x}} {{nonijus.D.y}} l {{nonijus.width*.005}} {{nonijus.height*.066}}'+
  'A{{nonijus.width*.05}},{{nonijus.width*.05}} 0 0,0 {{nonijus.L.x}},{{nonijus.L.y}} l0,{{-nonijus.height*0.12}} z"'+
  ' stroke="#a3a3c2" stroke-width="1" fill="#a3a3c2" />'+
'<rect  ng-attr-x="{{nonijus.L.x-nonijus.width*.007}}" ng-attr-y="{{nonijus.L.y-nonijus.height*.1}}"'+
'ng-attr-width="{{nonijus.width*.007}}" ng-attr-height="{{nonijus.height*.09}}" '+
'style="fill:rgb(117, 117, 163);stroke-width:1;stroke:rgb(117, 117, 163))" />'+
'<path  ng-attr-d="M {{nonijus.A.x}} {{nonijus.A.y}} '+
  'A{{nonijus.width*.05}},{{nonijus.width*.1}} 0 0,0 {{nonijus.M.x}},{{nonijus.M.y}} l0,{{nonijus.height*0.16}}'+
  'l{{nonijus.width*.002}},0 l0,{{nonijus.height*0.04}} z"'+
  ' stroke="#a3a3c2" stroke-width="1" fill="#a3a3c2" />'+
'<path  ng-attr-d="M {{nonijus.M.x}} {{nonijus.M.y}} l0,{{nonijus.height*0.16}} '+
'l{{nonijus.width*.006}},0 l0,{{-nonijus.height*0.125}} '+
  'A{{nonijus.width*.05}},{{nonijus.width*.1}} 0 0,0 {{nonijus.M.x}},{{nonijus.M.y}} l0,{{nonijus.height*0.16}}"'+  
  ' stroke="rgb(117, 117, 163)" stroke-width="1" fill="rgb(117, 117, 163)" />'+ 
  '<path class="slider" ng-attr-d="M {{nonijus.H.x + pomak+nonijus.width*0.01}} {{nonijus.H.y}} '+
  'l{{nonijus.width*0.216}},0 l0,{{nonijus.height*0.133}}'+
  'l{{-nonijus.width*0.008}},{{nonijus.height*.04}}'+
  'l{{-nonijus.width*0.02}},0 l{{-nonijus.width*0.008}},{{-nonijus.height*.04}}'+
  'l{{-nonijus.width*0.142}},0 l{{-nonijus.width*0.02416}},{{nonijus.height*.348}}'+
  'A{{nonijus.width*.05}},{{nonijus.width*.03}} 0 0,1 {{nonijus.N.x}},{{nonijus.N.y}} l0,{{-nonijus.height*0.16}}'+
  'l{{nonijus.width*.002}},0 l0,{{nonijus.height*0.04}} '+
  'l0,{{-nonijus.height*0.24}} l{{nonijus.width*0.005}},0 z"'+
  ' stroke="#a3a3c2" stroke-width="1" fill="#a3a3c2" />'+
  '<rect class="slider" ng-attr-x="{{nonijus.L.x + pomak}}" ng-attr-y="{{nonijus.L.y-nonijus.height*.1}}"'+
'ng-attr-width="{{nonijus.width*.007}}" ng-attr-height="{{nonijus.height*.09}}" '+
'style="fill:rgb(117, 117, 163);stroke-width:1;stroke:rgb(117, 117, 163)" />'
for(var i = 0;i <= 190;i++){
if(Math.floor(i/10)*10 == i){
var h = 0.067
telo += '<text ng-attr-x="{{nonijus.H.x +'+i+'*nonijus.width*.004 + nonijus.width*.016}}" '+
'ng-attr-y="{{nonijus.H.y - nonijus.height*'+h*1.1+'}}"'+
'ng--attr-font-size="{{nonijus.height*.08}}" fill="red">'+i/10+'</text>';
}else if(Math.floor(i/5)*5 == i){ h = 0.04}else{h = 0.027}
telo += '<line ng-attr-x1="{{nonijus.H.x +'+i+'*nonijus.width*.004 + nonijus.width*.016}}" ng-attr-y1="{{nonijus.H.y}}"'+
' ng-attr-x2="{{nonijus.H.x +'+i+'*nonijus.width*.004 + nonijus.width*.016}}" ng-attr-y2="{{nonijus.H.y - nonijus.height*'+h+'}}"'+
' style="stroke:black;stroke-width:1" />';
};
for(var i = 0;i <= 50;i++){
if(Math.floor(i/5)*5 == i){
var h = 0.067; var l = i/5;
if(l == 10){l = 0;}
telo += '<text ng-attr-x="{{nonijus.H.x +'+i+'*nonijus.width*.004*49/50 + nonijus.width*.016 + pomak}}" '+
'ng-attr-y="{{nonijus.H.y + nonijus.height*'+h*1.4+'}}"'+
'ng--attr-font-size="{{nonijus.height*.07}}" fill="red">'+l+'</text>';
}else{h = 0.027}
telo += '<line ng-attr-x1="{{nonijus.H.x +'+i+'*nonijus.width*.004*49/50 + nonijus.width*.016 + pomak}}" ng-attr-y1="{{nonijus.H.y}}"'+
' ng-attr-x2="{{nonijus.H.x +'+i+'*nonijus.width*.004*49/50 + nonijus.width*.016 + pomak}}" ng-attr-y2="{{nonijus.H.y + nonijus.height*'+h+'}}"'+
'  style="stroke:black;stroke-width:1" />';
};
telo += '</g>';
return telo;
}
//Zavrtanj
//Nonijus
 app.directive('zavrtanj', function($compile,$interval) {
 
   function link(element,attr){
   console.log('pre',element);
  //Definisanje strukture elementa
  var Telo = Zavrtanj();
  return Telo;
    };
    function povezi(scope,element,attr){
scope.yp2 = [];scope.yp1 = [];scope.yd1 = [];scope.yd3 = [];scope.yd4 = [];
scope.yo1 = []; scope.yo2 = [];scope.yd2 = [];scope.linija3 = [];
scope.h = []; 
 element.on("dodir",function(event,log,q1,q2){
 
 });// Kraj mouse on
element.dblclick(function(event){
scope.zaustavi = true;
}); 
element.mousedown(function(event){
var selekcija = $(event.target)
if(selekcija.attr("class") == 'klizac'){
scope.okretanje = true;
scope.zaustavi = false;
} 
});
element.mouseup(function(event){

});
   element.mousemove(function(event){

     });//Kraj mousemove
 //Obrtanje vijka
element.on("okreni",function(ev,ugao){
if(ugao != 0){scope.sgn = ugao/Math.abs(ugao);};
if(scope.phi >= 0){
scope.theOldTime = new Date().getTime();
var time = $interval(function (ev) {
      scope.theTime = new Date().getTime();
//Tekuće vreme
scope.t = (scope.theTime - scope.theOldTime)/1000;
scope.phi += 0.05*2*Math.PI*scope.sgn;
if(Math.cos(scope.phi) < 0){
scope.linija = false;scope.linija1 = true;
}else{scope.linija = true;scope.linija1 = false;
};
var phi = 280*.45*2*Math.PI;
var korak = 0.5/140*scope.zavrtanj.width;
scope.duzina = korak*scope.phi/2/Math.PI;
for(var i = -80;i <= 80;i++){
scope.yp2[i] = 2*scope.zavrtanj.height*Math.sin(-scope.zavrtanj.width*(1-i/5)*.143/2/scope.zavrtanj.height + scope.phi);
scope.yp1[i] = 2*scope.zavrtanj.height*Math.sin(scope.zavrtanj.width*.143*(1+i/5)/2/scope.zavrtanj.height + scope.phi)
scope.yo2[i] = 2*scope.zavrtanj.height*Math.sin(scope.zavrtanj.width*(1-i/5)*.143/2/scope.zavrtanj.height + scope.phi);
scope.yo1[i] = 2*scope.zavrtanj.height*Math.sin(-scope.zavrtanj.width*.143*(1+i/5)/2/scope.zavrtanj.height + scope.phi)
};
for(var i = 0;i < 50;i++){
if(Math.cos(scope.phi - i*2*Math.PI/50) >= 0){scope.linija3[i] = true
}else{scope.linija3[i] = false;};
scope.yd2[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.28*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.yd1[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + Math.sin(scope.phi - i*2*Math.PI/50));
scope.yd3[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.42*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.yd4[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.7*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.h[i] = Math.abs(Math.cos(scope.phi - i*2*Math.PI/50));
};
if(scope.phi > phi ){scope.zaustavi = true;}
if(scope.phi < 0){scope.zaustavi = true;}
if(scope.duzina <= scope.mereni.width && scope.contact){
  scope.duzina = scope.mereni.width; 
if(scope.sgn < 0){scope.zaustavi = true;};
  };
if(scope.zaustavi){
$interval.cancel( time);
if(scope.phi < 0){scope.phi = 0;scope.zaustavi = false;}
if(scope.phi > phi){scope.phi = phi;scope.zaustavi = false;};
}
 }, 20);
}//Kraj if-phi > 0

});
// ažuriranje zavrtnja    
element.on("pokazi",function(){
for(var i = -80;i <= 80;i++){

scope.yp2[i] = 2*scope.zavrtanj.height*Math.sin(-scope.zavrtanj.width*(1-i/5)*.143/2/scope.zavrtanj.height + scope.phi);
scope.yp1[i] = 2*scope.zavrtanj.height*Math.sin(scope.zavrtanj.width*.143*(1+i/5)/2/scope.zavrtanj.height + scope.phi)
scope.yo2[i] = 2*scope.zavrtanj.height*Math.sin(scope.zavrtanj.width*(1-i/5)*.143/2/scope.zavrtanj.height + scope.phi);
scope.yo1[i] = 2*scope.zavrtanj.height*Math.sin(-scope.zavrtanj.width*.143*(1+i/5)/2/scope.zavrtanj.height + scope.phi)
};

scope.zavrtanj.A.x = scope.zavrtanj.x + scope.zavrtanj.width*0.5002;
scope.zavrtanj.A.y = scope.zavrtanj.y + scope.zavrtanj.height*0.3846;
scope.zavrtanj.B.x = scope.zavrtanj.x + scope.zavrtanj.width*0.0143;
scope.zavrtanj.B.y = scope.zavrtanj.y + scope.zavrtanj.height*0.4764;
scope.zavrtanj.C.x = scope.zavrtanj.x + scope.zavrtanj.width*0.129;
scope.zavrtanj.C.y = scope.zavrtanj.y + scope.zavrtanj.height*0.42;
scope.zavrtanj.D.x = scope.zavrtanj.x + scope.zavrtanj.width*0.53;
scope.zavrtanj.D.y = scope.zavrtanj.C.y;
scope.zavrtanj.E.x = scope.zavrtanj.x + scope.zavrtanj.width*0.55;
scope.zavrtanj.E.y = scope.zavrtanj.y + scope.zavrtanj.height*0.42;
scope.zavrtanj.F.x = scope.zavrtanj.x + scope.zavrtanj.width*0.107;
scope.zavrtanj.F.y = scope.zavrtanj.E.y;
scope.zavrtanj.G.x = scope.zavrtanj.x + scope.zavrtanj.width*.143;
scope.zavrtanj.G.y = scope.zavrtanj.y + scope.zavrtanj.height*0.0922;
scope.zavrtanj.H.x = scope.zavrtanj.G.x + scope.zavrtanj.width*0.05;
scope.zavrtanj.H.y = scope.zavrtanj.G.y;
scope.zavrtanj.I.x = scope.zavrtanj.G.x + scope.zavrtanj.width*0.5153;
scope.zavrtanj.I.y = scope.zavrtanj.y + scope.zavrtanj.height*0.0307;
scope.zavrtanj.J.x = scope.zavrtanj.I.x + scope.zavrtanj.width*0.05;
scope.zavrtanj.J.y = scope.zavrtanj.I.y - scope.zavrtanj.height*0.07;
scope.zavrtanj.K.x = scope.zavrtanj.J.x + scope.zavrtanj.width*0.085;
scope.zavrtanj.K.y = scope.zavrtanj.J.y ;
scope.zavrtanj.L.x = scope.zavrtanj.K.x + scope.zavrtanj.width*0.143;
scope.zavrtanj.L.y = scope.zavrtanj.K.y ;
scope.zavrtanj.M.x = scope.zavrtanj.L.x + scope.zavrtanj.width*0.05;
scope.zavrtanj.M.y = scope.zavrtanj.L.y + scope.zavrtanj.height*0.07;
scope.zavrtanj.N.x = scope.zavrtanj.M.x + scope.zavrtanj.width*0.057;
scope.zavrtanj.N.y = scope.zavrtanj.M.y ;
scope.zavrtanj.O.x = scope.zavrtanj.N.x + scope.zavrtanj.width*0.05;
scope.zavrtanj.O.y = scope.zavrtanj.J.y ;
scope.zavrtanj.P.x = scope.zavrtanj.O.x + scope.zavrtanj.width*0.057;
scope.zavrtanj.P.y = scope.zavrtanj.J.y ;
scope.zavrtanj.Q.x = scope.zavrtanj.I.x;
scope.zavrtanj.Q.y = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1;
scope.zavrtanj.R.x = scope.zavrtanj.Q.x + scope.zavrtanj.width*0.45;
scope.zavrtanj.R.y = scope.zavrtanj.Q.y - scope.zavrtanj.height*0.02;
scope.zavrtanj.S.y = scope.zavrtanj.Q.y - scope.zavrtanj.height*0.04;
scope.zavrtanj.T.y = scope.zavrtanj.Q.y - scope.zavrtanj.height*0.03;
for(var i = 0;i < 50;i++){
if(Math.cos(scope.phi - i*2*Math.PI/50) > 0){scope.linija3[i] = true
}else{scope.linija3[i] = false;};
scope.yd2[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.28*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.yd1[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + Math.sin(scope.phi - i*2*Math.PI/50));
scope.yd3[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.42*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.yd4[i] = scope.zavrtanj.I.y + scope.zavrtanj.height*0.1*(1 + 1.7*Math.sin(scope.phi - i*2*Math.PI/50)) ;
scope.h[i] = Math.abs(Math.cos(scope.phi - i*2*Math.PI/50));
};
}); //Kraj pokazi  
    };//Kraj povezi
    return {
      templateNamespace: 'svg',
      restrict: 'E',
      replace: true,
      template: link,
      link:povezi,
      
      //transclude:true,
      
    };
});   
//Telo zavrtnja
function Zavrtanj(){
var telo = '<g   ng-show="zavrtanj.jeKreiran" ng-mousedown="elementMouseDown($event)" '+
'ng-mouseleave= "mouseLeave()" ng-mouseenter="mouseEnter()"' +
'ng-attr-transform="'+
'rotate({{zavrtanj.rotation.degree}}, {{zavrtanj.rotation.x}}, {{zavrtanj.rotation.y}})">' +
'<rect class="klizac" ng-attr-x="{{zavrtanj.H.x + duzina}}" ng-attr-y="{{zavrtanj.H.y}}"'+
  'ng-attr-width="{{zavrtanj.width*.45}}" ng-attr-height="{{zavrtanj.height*.107}}" '+
  'style="fill:#80a3c2;stroke-width:1;stroke:#80a3c2" />'+
'<rect  ng-attr-x="{{zavrtanj.I.x }}" ng-attr-y="{{zavrtanj.I.y}}"'+
  'ng-attr-width="{{zavrtanj.width*.46}}" ng-attr-height="{{zavrtanj.height*.2}}" '+
  'style="fill:#bba3c2;stroke-width:1;stroke:#bba3c2" />'+  
  '<line  ng-attr-x1="{{zavrtanj.Q.x}}" ng-attr-x2="{{zavrtanj.R.x}}" ng-attr-y1="{{zavrtanj.Q.y}}" ng-attr-y2="{{zavrtanj.Q.y}}" style="stroke: black; " />';
for(var i = 0; i <= 126;i++){
if(Math.floor(i/2)*2 == i){
telo += '<line  ng-attr-x1="{{zavrtanj.Q.x + '+i+'*.5/140*zavrtanj.width}}" ng-attr-x2="{{zavrtanj.Q.x +'+i+'*.5/140*zavrtanj.width}}" ng-attr-y1="{{zavrtanj.Q.y}}" ng-attr-y2="{{zavrtanj.T.y}}" style="stroke: black;stroke-width:0.5 " />';
}else{
telo += '<line  ng-attr-x1="{{zavrtanj.Q.x + '+i+'*.5/140*zavrtanj.width}}" ng-attr-x2="{{zavrtanj.Q.x +'+i+'*.5/140*zavrtanj.width}}" ng-attr-y1="{{zavrtanj.Q.y}}" ng-attr-y2="{{zavrtanj.R.y}}" style="stroke: black;stroke-width:0.5 " />';
};
if(Math.floor(i/10)*10 == i){
telo += '<text ng-attr-x="{{zavrtanj.Q.x + '+i+'*.5/140*zavrtanj.width}}" '+
'ng-attr-y="{{zavrtanj.S.y}}"'+
'ng--attr-font-size="{{zavrtanj.height*.02}}" fill="red">'+i/2+'</text>' +
'<line  ng-attr-x1="{{zavrtanj.Q.x + '+i+'*.5/140*zavrtanj.width}}" ng-attr-x2="{{zavrtanj.Q.x +'+i+'*.5/140*zavrtanj.width}}" ng-attr-y1="{{zavrtanj.Q.y}}" ng-attr-y2="{{zavrtanj.S.y}}" style="stroke: black;stroke-width:0.5 " />';
};
};
telo += '<path  ng-attr-d="M {{zavrtanj.x}} {{zavrtanj.y}} l{{zavrtanj.width*.143}},0'+
' l0 {{zavrtanj.height*.3846}}'+
  ' A{{zavrtanj.width*.357}},{{zavrtanj.height*.4}} 0 0,0 {{zavrtanj.A.x}},{{zavrtanj.A.y}} l0 {{-zavrtanj.height*0.3846}} '+
  ' l{{zavrtanj.width*.143}},0 l{{zavrtanj.width*.0143}},{{zavrtanj.height*.0307}} '+
  ' l0 {{zavrtanj.height*.23}} l{{-zavrtanj.width*.0143}},{{zavrtanj.height*.0307}} '+
  ' l0,{{zavrtanj.height*.2}} '+
  ' A{{zavrtanj.width*.5}},{{zavrtanj.height*.9846}} 0 0,1 {{zavrtanj.B.x}},{{zavrtanj.B.y}} '+
  ' l0,{{-zavrtanj.height*.2}} l{{-zavrtanj.width*.0143}},{{-zavrtanj.height*.0307}} z"'+
  ' stroke="#a3a3c2" stroke-width="1" fill="#a3a3c2" />'+
  '<path  ng-attr-d="M {{zavrtanj.C.x}} {{zavrtanj.C.y}} '+
  ' A{{zavrtanj.width*.382}},{{zavrtanj.height*.48}} 0 0,0 {{zavrtanj.D.x}},{{zavrtanj.D.y}}  '+
  ' A{{zavrtanj.width*.005}},{{zavrtanj.width*.005}} 0 0,1 {{zavrtanj.E.x}},{{zavrtanj.E.y}}  '+
  ' A{{zavrtanj.width*.18}},{{zavrtanj.height*0.15}} 0 0,1 {{zavrtanj.F.x}},{{zavrtanj.F.y}} '+
  ' A{{zavrtanj.width*.005}},{{zavrtanj.width*.0051}} 0 1,1 {{zavrtanj.C.x}},{{zavrtanj.C.y}} "'+
  ' stroke="#29293d" stroke-width="1" fill="##29293d" />';
telo += '<rect  ng-attr-x="{{zavrtanj.G.x }}" ng-attr-y="{{zavrtanj.G.y}}"'+
'ng-attr-width="{{zavrtanj.width*.05}}" ng-attr-height="{{zavrtanj.height*.107}}" '+
'style="fill:#80a3c2;stroke-width:1;stroke:#80a3c2" />';
telo += '<path class="klizac" ng-attr-d="M {{zavrtanj.I.x + duzina}} {{zavrtanj.I.y}} '+
'l{{zavrtanj.width*.05}},{{-zavrtanj.height*.07}} l0,{{zavrtanj.height*.34}}'+ 
'l{{-zavrtanj.width*.05}},{{-zavrtanj.height*.07}} z"'+
  ' stroke="#d1d1e0" stroke-width="1" fill="url(#skala)" />';
for(var i = 0; i < 50; i++){
if(Math.floor(i/5)*5 == i){
telo += '<line ng-show="linija3['+i+']" ng-attr-x1="{{zavrtanj.I.x + duzina}}" ng-attr-x2="{{zavrtanj.I.x + zavrtanj.width*.03 + duzina}}" ng-attr-y1="{{yd1['+i+']}}" ng-attr-y2="{{yd3['+i+']}}" style="stroke: black; " />';
}else{
telo += '<line ng-show="linija3['+i+']" ng-attr-x1="{{zavrtanj.I.x + duzina}}" ng-attr-x2="{{zavrtanj.I.x + zavrtanj.width*.02 + duzina}}" ng-attr-y1="{{yd1['+i+']}}" ng-attr-y2="{{yd2['+i+']}}" style="stroke: black; " />';
}
};  
telo += '<rect class="klizac" ng-attr-x="{{zavrtanj.J.x + duzina}}" ng-attr-y="{{zavrtanj.J.y}}"'+
  'ng-attr-width="{{zavrtanj.width*.085}}" ng-attr-height="{{zavrtanj.height*.34}}" '+
  'style="fill:#c3c3d5;stroke-width:1;stroke:#c3c3d5" />'; 
for(var i = 0;i < 50;i++){ 
if(Math.floor(i/5)*5 == i){
telo+= '<text ng-show="linija3['+i+']" ng-attr-x="{{zavrtanj.J.x + duzina}}" '+
'ng-attr-y="{{yd4['+i+']}}"'+
'ng--attr-font-size="{{zavrtanj.height*.02*h['+i+']}}" fill="red">'+i+'</text>';
}
}
telo+= '<defs>'+
  '<pattern id="transformedPattern"'+
'x="10" y="0" ng-attr-width="{{zavrtanj.width*.143}}" ng-attr-height="{{zavrtanj.height*.34}}"'+
         'patternUnits="userSpaceOnUse">';
telo += '<rect  x="0" y="0"'+
  'ng-attr-width="{{zavrtanj.width*.143}}" ng-attr-height="{{zavrtanj.height*.34}}" '+
  'style="fill:#9696b6;stroke-width:1;stroke:#9696b6" />';         
for(var i = -80;i <= 80;i++){
 telo += '<line ng-show="linija" x1="0" ng-attr-x2="{{zavrtanj.width*.143}}" ng-attr-y1="{{yo1['+i+']}}" ng-attr-y2="{{yo2['+i+']}}" style="stroke: #c2c2d6; " />'+
 '<line ng-show="linija1" x1="0" ng-attr-x2="{{zavrtanj.width*.143}}" ng-attr-y1="{{-yo1['+i+']}}" ng-attr-y2="{{-yo2['+i+']}}" style="stroke: #c2c2d6; " />'+
 '<line ng-show="linija" x1="0" ng-attr-x2="{{zavrtanj.width*.143}}" ng-attr-y1="{{yp1['+i+']}}" ng-attr-y2="{{yp2['+i+']}}" style="stroke: #c2c2d6; " />'+
 '<line ng-show="linija1" x1="0" ng-attr-x2="{{zavrtanj.width*.143}}" ng-attr-y1="{{-yp1['+i+']}}" ng-attr-y2="{{-yp2['+i+']}}" style="stroke: #c2c2d6; " />';
}; 
telo += ' </pattern>';
telo += '<pattern id="skala"'+
         'x="0" y="0" ng-attr-width="{{zavrtanj.width*0.05}}" ng-attr-height="{{zavrtanj.height*.34}}"'+
         'patternUnits="userSpaceOnUse" > ';
telo += '<rect x="0" y="0" ng-attr-width="{{zavrtanj.width*.05}}" '+
' ng-attr-height="{{zavrtanj.height*.34}}"'+ 
  ' stroke="#d1d1e0" stroke-width="1" fill="#d1d1e0" />';         
telo += '</pattern> ';
telo += '</defs>';  
telo += '<rect class="klizac" ng-attr-x="{{zavrtanj.K.x + duzina}}" ng-attr-y="{{zavrtanj.K.y}}"'+
  'ng-attr-width="{{zavrtanj.width*.143}}" ng-attr-height="{{zavrtanj.height*.34}}" '+
  'style="fill:url(#transformedPattern);stroke-width:1;stroke:#9696b6" />'+
  '<path class="klizac" ng-attr-d="M {{zavrtanj.L.x + duzina}} {{zavrtanj.L.y}} '+
'l{{zavrtanj.width*.05}},{{zavrtanj.height*.07}} l0,{{zavrtanj.height*.2}}'+ 
'l{{-zavrtanj.width*.05}},{{zavrtanj.height*.07}} z"'+
' stroke="#d1d1e0" stroke-width="1" fill="#d1d1e0" />'+
'<rect class="klizac" ng-attr-x="{{zavrtanj.M.x + duzina}}" ng-attr-y="{{zavrtanj.M.y}}"'+
  'ng-attr-width="{{zavrtanj.width*.057}}" ng-attr-height="{{zavrtanj.height*.2}}" '+
  'style="fill:#c3c3d5;stroke-width:1;stroke:#c3c3d5" />'+
  '<path class="klizac" ng-attr-d="M {{zavrtanj.N.x + duzina}} {{zavrtanj.N.y}} '+
'l{{zavrtanj.width*.05}},{{-zavrtanj.height*.07}} l0,{{zavrtanj.height*.34}}'+ 
'l{{-zavrtanj.width*.05}},{{-zavrtanj.height*.07}} z"'+
  ' stroke="#d1d1e0" stroke-width="1" fill="#d1d1e0" />'+
'<rect class="klizac" ng-attr-x="{{zavrtanj.O.x + duzina}}" ng-attr-y="{{zavrtanj.O.y}}"'+
'ng-attr-width="{{zavrtanj.width*.057}}" ng-attr-height="{{zavrtanj.height*.34}}" '+
 'style="fill:url(#transformedPattern);stroke-width:1;stroke:#9696b6" />'+
'<path class="klizac" ng-attr-d="M {{zavrtanj.P.x + duzina}} {{zavrtanj.P.y}} '+
'l{{zavrtanj.width*.05}},{{zavrtanj.height*.07}} l0,{{zavrtanj.height*.2}}'+ 
'l{{-zavrtanj.width*.05}},{{zavrtanj.height*.07}} z"'+
' stroke="#d1d1e0" stroke-width="1" fill="#d1d1e0" />'
telo += '</g>';
return telo;
}
//Metar
app.directive('metar', function() {
    function link(element,attr){
if(attr.x0==null){attr.x0 = 100;};
if(attr.y0==null){attr.y0 = 100;};
if(attr.opacityBaze==null){attr.opacityBaze = 1;};
if(attr.opacityOmotaca==null){attr.opacityOmotaca = 1;};
if(attr.sirinaLinijeBaze==null){attr.sirinaLinijeBaze = 1;};
if(attr.sirinaLinije==null){attr.sirinaLinije = 1;};
if(attr.bojaBaze==null){attr.bojaBaze = "yellow";};
if(attr.bojaOmotaca==null){attr.bojaOmotaca = "green";};
if(attr.bojaLinije==null){attr.bojaLinije = "blue";};
 var telo = Metar(attr.x0*1,attr.y0*1,attr.theta0*1,attr.theta*1,
 attr.phi*1,attr.r*1,attr.h*1,attr.bojaBaze,attr.bojaOmotaca,
 attr.bojaLinije,attr.opacityBaze,attr.opacityOmotaca,attr.sirinaLinije,attr.sirinaLinijeBaze);
 return telo;
  };
  
    return {
      templateNamespace: 'svg',
      restrict: 'E',
      replace: true,
      template:link
      
    };
})
//Radna funkcija metra
function Metar(x0,y0,theta0,theta,phi,R,H,bojaBaze,bojaOmotaca,
bojaLinije,opacityBaze,opacityOmotaca,sirinaLinije,sirinaLinijeBaze){
var theta = Math.PI/180*theta;
var theta0 = theta0*Math.PI/180;
var phi = Math.PI/180*phi;
var telo = '<g>';
telo += '<polygon ng-show="{{metar.prviShow}}" points="{{metar.A.x}},{{metar.A.y}} {{metar.B.x}},{{metar.B.y}} {{metar.C.x}},{{metar.C.y}} {{metar.D.x}},{{metar.D.y}}" style="fill:'+bojaOmotaca+
';stroke:purple;stroke-width:1" />';
telo += '<polygon ng-show="{{metar.drugiShow}}" points="{{metar.A.x}},{{metar.A.y}} {{metar.B.x}},{{metar.B.y}} {{metar.F.x}},{{metar.F.y}} {{metar.E.x}},{{metar.E.y}}" style="fill:'+bojaBaze+
';stroke:purple;stroke-width:1" />';
telo += '<polygon ng-show="{{metar.treciShow}}" points="{{metar.B.x}},{{metar.B.y}} {{metar.F.x}},{{metar.F.y}} {{metar.G.x}},{{metar.G.y}} {{metar.C.x}},{{metar.C.y}}" style="fill:'+bojaOmotaca+
';stroke:purple;stroke-width:1" />';
telo += '<polygon ng-show="{{metar.forthShow}}" points="{{metar.E.x}},{{metar.E.y}} {{metar.F.x}},{{metar.F.y}} {{metar.G.x}},{{metar.G.y}} {{metar.H.x}},{{metar.H.y}}" style="fill:'+bojaOmotaca+
';stroke:purple;stroke-width:1" />';
telo += '<polygon ng-show="{{metar.fifthShow}}" points="{{metar.A.x}},{{metar.A.y}} {{metar.E.x}},{{metar.E.y}} {{metar.H.x}},{{metar.H.y}} {{metar.D.x}},{{metar.D.y}}" style="fill:'+bojaOmotaca+
';stroke:purple;stroke-width:1" />';
telo += '<polygon ng-show="{{metar.sixthShow}}" points="{{metar.D.x}},{{metar.D.y}} {{metar.H.x}},{{metar.H.y}} {{metar.G.x}},{{metar.G.y}} {{metar.C.x}},{{metar.C.y}}" style="fill:'+bojaBaze+
';stroke:purple;stroke-width:1" />';
var d = 3;
for(var k = 0;k <= 80;k++){
var z = 12;var boja = "rgb(5,0,0)";
if(k == 5*Math.round(k/5)){var z = 15;}
if(k == 10*Math.round(k/10)){var z = 20;}
if(k == 40){var boja = "rgb(255,0,0)";};
var x1 = x0 + k*d*Math.cos(theta0)*Math.cos(phi);
var x2 = x0 + k*d*Math.cos(theta0)*Math.cos(phi) + z*Math.sin(theta0)*Math.cos(phi);
var y1 = y0 + k*d*(Math.sin(theta0)*Math.sin(theta) + Math.cos(theta0)*Math.cos(theta)*Math.sin(phi));
var y2 = y1 - z*(Math.cos(theta0)*Math.sin(theta) - Math.sin(theta0)*Math.cos(theta)*Math.sin(phi));
telo += ' <line x1="'+x1+'" y1="'+y1+'" x2="'+x2+'" y2="'+y2+'" style="stroke:'+boja+';stroke-width:1" />';
};
telo += '</g>';
return telo
}

</script>


