Day 140 — Phishing Analysis Fundamentals
Platform: TryHackMe
Module: SOC Level 1 — Phishing Analysis
Date: [fecha]

Summary
This room covers the fundamentals of phishing email analysis, focusing on how to identify malicious emails by examining their components: sender, headers, body, and attachments.

What the attack looks like
A phishing attack starts with a carefully crafted email designed to trick the recipient into taking an action — clicking a link, downloading a file, or providing credentials. The attacker spoofs a trusted sender, creates urgency, and hides the real destination behind legitimate-looking text.

Key concepts reviewed
Email headers are the most important part of analysis. The visible "From" field can be completely faked. What actually matters is:

Return-Path — where bounced emails go, often reveals the real sender domain
Received — the chain of servers the email passed through, read bottom to top
X-Originating-IP — the IP where the email actually originated
Reply-To — if different from From, that's a red flag

Defanging — when documenting IOCs (indicators of compromise) we write URLs and IPs in a defanged format so they can't be accidentally clicked. http://malicious.com becomes hxxp[://]malicious[.]com

What I actually understood
Antes de rehacer esta room pensaba que analizar un email de phishing era ver si el remitente parecía raro. Ahora entiendo que el campo From no significa nada por sí solo porque es trivial de falsificar. Lo que realmente dice la verdad son los headers técnicos, especialmente el campo Received que muestra el camino real que hizo el email por los servidores. Si el email dice venir de paypal.com pero el Received muestra un servidor en un dominio random, ahí está la trampa.

IOCs identified (example)
TypeValueDefangedSender IP192.168.1.1192[.]168[.]1[.]1Malicious URLhttp://fake-paypal.com/loginhxxp[://]fake-paypal[.]com/loginReply-Toattacker@gmail.comattacker[@]gmail[.]com

Tools used

Email header analyzers — MXToolbox, Google Admin Toolbox
URL scanners — VirusTotal, URLScan.io
Manual header inspection


Difficulty & gaps identified
Lo que no me quedó del todo claro: cómo determinar con certeza si un dominio es reciente (recién registrado = sospechoso). Necesito practicar más con WHOIS lookup.