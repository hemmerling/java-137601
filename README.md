# java-137601
- java-137601 ( OCEJWCD 6, 1Z0-899 ).
## Notizen zum Kurs, Lecture Notes
### Annotationen ###
- Annotationen sind "neu" in Java EE 6. In Java EE 5 noch nicht vorhanden, also auch nicht im Java EE5 Lernmaterial.
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
## Laufzeitumgebung ##
- Tomcat benötigt immer einen JDK, eine JRE reicht nicht aus
## HttpServlet ##
- „Cookies sind nicht anderes als Headers“ => Session Management HttpRequest
- httpServletRequest() => getCookies()
- HttpServletRequest (1) vs HttpServletResponse(2)
  1. GetHeaderNames => Enumeration, Header sind nur lesbar
  2. Collection<String>, Modifizieren des Headers möglich ( Response !!)
- Context-parameter nur in init() im Servlet setzbar
## Netbeans IDE nennt zur Verfügung stehende Objekte ##
- Auto-Complete in Netbeans  CTRL + SPACE
- Wenn man in einem leeren <% %> CTRL+SPACE eingibt, erhält man alle Basisobjekte, die in JSP Seiten  zur Verfügung stehen, wie z.B. request, response, session, application ( vom Typ ServletContext, für Context-Methoden  )
## Pages ##
- Request- und PageContext Attribute sind threadsafe.
- Session- und Context-Attribute sind beide NICHT threadsafe:
  1. Peter kann zwei Session Attribute erhalten, wenn er nacheinander in verschiedenen Browser-Tabs/Fenstern eine Anfrage losschickt,
  2. Hilfestellung: Die erste Anfrage dauert länger, dann bekommt auf jeden Fall auch die zuerst behandelte, aber zweite Anfrage eine eigenes Session Attribut
  3. Zwei verschiedene Anfragen können die auf die selben Context-Attribute zugreifen. 
- PageContext gibt es nur für JSP Seiten , nicht für Servlets. Es ist eine lokale Variable/Objekt das durch Aufruf einer JSP Seite entsteht und lebt kürzer als ein Request. Jede Anfrage hat ein PageContext. Nutzung in JSP seite für die Wiederverwendbarkeit von graphischen Objekten ( Bildern..) innerhalb einer JP-Seite
## Synchronisierung von 2 Servlets S1, S2 ##
- Keine Lösung, die Methoden „synchronize doGet ()“ werden nicht blockiert, ein Thread kann doget() von S1, ein anderer Thread doGet() von S2 ausführen.
- Lösung: Synchronisierung über gemeinsame Objekte ( synchronized(session) bzw. synchronized(context) )
## Servlet Lifecyle ##
- Servlet Lifecyle
  1. Class Loading
  2. Instantiation
  3. Initalisation
  4. Service
  5. Destruction
- aber im gleichen Code kann man im gleichen Callstack nur 1x Forwarden !!
- Kein Problem von Servlet zu Servlet zu forwarden 
## Context Attributes ##
- org.apache.tomcat.util.scan.MergedWebXml => WEB-INF/web.xml warden hier auch mit gelistet ( “gemerged” )
- Tomcat-ContextAttributes enthalten immer einen Punkt ( „.“ eines Klassenpfads ), wenn man nur die eigene Attribute möchte, dann die mit Punkt ausschließen
## Scopes ##
- pageContext.getAttribute("Test", pageContext.APPLICATION_SCOPE           )  
- Object attributeValue = pageContext.getAttributes(attributeName, PageContext.APPLICATION_SCOPE);
## Servlet-Konfiguration mit Annotationen ##
- Der Name eines Servlets hat einen Defaultwert, den vollen Klassennamen der Servlet-Klasse.
- Wichtig ist ist der „urlPatterns“, damit das Servlet gefunden wird
## Listener ##
- Listener
  - ServeletContextListener 
    - contextIntialized() - Wird erzeugt beim Deployen der Applikation aufgerufen ( 1x Pro Anwendung ausführen)
    - contextDestroyed() – Beim Undeployen der Applikation
  - httpSessionListener
    - sessionCreated() – wird aufgerufen beim erstmaligen Anmelden eines Benutzers ( 1x pro Benutzer ausführen)
    - sessionDestroyed() – bei Timeout (30 min Default-Wert ), bei explizitem Schließen durch „Abmelden“ des Benutzers durch eine Applikationsfunktion
  - ServletRequestListener
    - requestInitialized – 1x pro Anfrage
- Wichtige Design-Regel: 1 Listener für jedes Thema ( also nur 1 Listener für ein Thema pro Applikation ), z.B. RequestAttribute
- Dynamische Registrierung von Listenern nur in der Startphase! Und: JSP-Seiten lassen sich nicht dynamisch registrieren

## Preparation Questions
### Actual K1-K4, Q2
- Q: Given an HttpServletRequest request and HttpServletResponse response, which sets a cookie "username" with the value "joe" in a servlet?
- A:**_response.addCookie_**(new Cookie("username", "joe"))
