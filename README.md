# java-137601
- java-137601 ( OCEJWCD 6, 1Z0-899 ).
## Notizen zum Kurs, Lecture Notes
### Tags ###
- Tag Files, Tag Handler = nicht mehr prüfungsrelevant für OCEJWCD 6.
### Request, Response ###
- Die HTTP-Methode (GET,.. ) wird nur im Request in der  “Request Line“ erwähnt, nicht bei der Response in der „Response Line“
- Catalina is Tomcat's servlet container.
- Jasper - JSP engine
- Coyote is a Connector component for Tomcat that supports the HTTP 1.1 protocol as a web server
- request.* Methoden sind fast alles Lese-Methoden ( z.B. request.setAttribute(…);###C
### JSP-Konfiguration, WEB-INF ###
- `<el-ignored>true</el-ignored>`  
  // Expression language ignored, d. h. Ignorieren von $Anweisungen in JSP-Seiten
- `<scripting-invalid>true</scripting-invalid>`
  // Gar kein Scripting auf JSP-Seiten
- Error – Handling in WEB-INF/web.xml

## Preparation Questions
### Actual K1-K4, Q2
- Q: Given an HttpServletRequest request and HttpServletResponse response, which sets a cookie "username" with the value "joe" in a servlet?
- A:**_response.addCookie_**(new Cookie("username", "joe"))
