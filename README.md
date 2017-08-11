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
1. `<el-ignored>true</el-ignored>`  
  // Expression language ignored, d. h. Ignorieren von $Anweisungen in JSP-Seiten
2. `<scripting-invalid>true</scripting-invalid>`
  // Gar kein Scripting auf JSP-Seiten
3. Error – Handling in WEB-INF/web.xml
##  Servlet/JSP - Lebenszyklus ##
- Design-Regel für die Methode init(ServletConfig): Meist gibt es in einer Anwendung nur eine ServletConfig, auch wenn eine Anwendung aus mehreren Servlets besteht.
- Init(ServletConfig) ruft init() auf
  - Jede Anfrage führt zu Thread-Objekt, jedes führt zur neuen service()-Aufruf. 
  - Mehrere Threads können gemeinsam ( also mehrfach !) auf die selben Instanz-Variablen zugreifen!
  - Konsistenz muss durch das Design der Anwendung sichergestellt werden
- Non-http Kommunikation per Oberklasse GenericServlet(), da gibt’s dann kein doGet() und doPost()
## Preparation Questions
### Actual K1-K4, Q2
- Q: Given an HttpServletRequest request and HttpServletResponse response, which sets a cookie "username" with the value "joe" in a servlet?
- A:**_response.addCookie_**(new Cookie("username", "joe"))
