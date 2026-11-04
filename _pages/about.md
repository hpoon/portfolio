---
layout: page
title: About
permalink: /about
comments: true
---

<div class="row justify-content-between">
  <div class="col-md-8 pr-5">
    <p>
      This is a quiet corner of the internet for technical hobbies, curious projects, and occasional rabbit holes.
    </p>

    <p>
      I’m a full-stack software engineer who spends most of his professional time on backend systems. I majored in mechatronics engineering, and early on in my career, I got to work across embedded software, hardware, and robotics-interests that still tend to follow me into my hobbies.
    </p>

    <p>
      I enjoy figuring out how things work, making them work better, and sometimes building something simply out of pure interest rather than any practical capitalistic free market purpose.
    </p>

    <p>
      My interests tend to land somewhere between software, hardware, home infrastructure, automation, and making physical things.  That can mean running services at home, working through some technical problem, designing something for the 3D printer, or simply something that interests me.
    </p>

    <p>
      Some are unfinished, some are complete, some are insignificant, and some may become something more later. What appears here is the part I decided to share.
    </p>

  </div>

  <div class="col-md-4">

    <div class="sticky-top sticky-top-80">
      <h5>Elsewhere</h5>

      <p>
        I am not especially active on social media. If you would like to
        get in touch, send me a message below.
      </p>

      <form id="contact-form" action="https://formspree.io/f/xwllaqpb" method="POST">
        <div class="form-group">
          <label for="contact-email">Your email</label>
          <input type="email" id="contact-email" name="email" class="form-control" required />
        </div>
        <div class="form-group">
          <label for="contact-message">Message</label>
          <textarea id="contact-message" name="message" class="form-control" rows="5" required></textarea>
        </div>
        <!-- Honeypot: hidden from people, bots tend to fill it -->
        <input type="text" name="_gotcha" style="display:none" tabindex="-1" autocomplete="off" />
        <button type="submit" class="btn btn-dark">Send</button>
        <p id="contact-status" role="status" class="mt-3"></p>
      </form>

      <script>
        (function () {
          var form = document.getElementById('contact-form');
          var status = document.getElementById('contact-status');
          var btn = form.querySelector('button[type="submit"]');
          form.addEventListener('submit', function (e) {
            e.preventDefault();
            btn.disabled = true;
            status.textContent = 'Sending…';
            fetch(form.action, {
              method: 'POST',
              body: new FormData(form),
              headers: { 'Accept': 'application/json' }
            }).then(function (res) {
              if (res.ok) {
                form.reset();
                status.textContent = 'Thanks! Your message has been sent.';
              } else {
                return res.json().then(function (data) {
                  status.textContent = (data.errors && data.errors.map(function (x) { return x.message; }).join(', ')) || 'Something went wrong. Please try again.';
                });
              }
            }).catch(function () {
              status.textContent = 'Something went wrong. Please try again.';
            }).finally(function () {
              btn.disabled = false;
            });
          });
        })();
      </script>
    </div>

  </div>
</div>
