Decision Support System Agent Framework

Intelligent agents are written in javascript and run on the server. The purpose of an agent application
is to parse historical and current data, using filters to set a price.

The notes below are intended for a javascript developer to build a repricing agent.

The javascript environment is a custom on built on top of the Mozilla SpiderMonkey engine.
There are several custom environment properties intended to help the DSS.

dss.username	: contains the account username
dss.product	: contains the product identifier for the base product record
dss.sku		: contains the specific SKU in focus
dss.strategy	: contains the name of the strategy being used 

Each strategy is comprised of a single file:
strategy.js


// this is javascript (as if it was loaded from a text file)
// log("URL is ", document.location.href);
log("username: "+dss.username);
log("pid: "+dss.product);
log("sku: "+dss.sku);


var p = product(dss.product);
log("zoovy:prod_name " + p.get("zoovy:prod_name"));
log("amz:catalog " + p.get("amz:catalog"));

var skus = p.skus();
log("skus: "+skus);

var d = new Date();
log("now is: "+d.toString());

var r = rpsku(dss.sku);
log("next: "+r.nextpoll());

var nextd = new Date(r.nextpoll());
log("nextd: "+nextd.toString());

var x = eval(r.toJSON());
// log("rpstring: "+r.toJSON());
for (i = 0; i<x.length; i++) {
   log(x[i][3].ship);
   }
