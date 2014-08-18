---
layout: post
title: "Kommentar zu 'Warnung vor dem Microservice'"
date: 2014-08-18 11:49:40 +0200
comments: true
categories: 
---

Die Warnung ist sicher angebracht, und inhaltlich kann ich zu allem zustimmen. Für mich ist ein etwas nebenbei angesprochener Aspekt grundlegend für die zurückhaltende Betrachtung der aktuellen Microservice Bewegung:

Einer der vielen Gründe dafür, dass SOA nicht die Erwartungen erfüllte, war sicherlich die enge Bindung von fachlicher Abgrenzung an physische (Deployment) Abgrenzung. Ähnliches in der klassischen Mehrschichtwelt auch gut bekannt unter dem Schlagwort "layers != tiers".

Dieselbe - in weiten Teilen sicherlich unreflektierte - Gleichsetzung sehe ich bei Microservices erneut. Was bringt es, einen Microservice zu bauen, der fachliche Abgrenzung und physische Laufzeitabgrenzung vereint? Was ist daran nachteilig?

Positiv ist sicherlich zunächst der Aspekt der fachlichen Abgrenzung überhaupt. Diese ermöglicht eine, passgenauere trennscharfe Entwicklung - bereits durch die Konzentration auf einen Aspekt, erleichtern das Neubauen-statt-Reparieren. Stichwort Bounded Context. Doch dafür benötige ich keine Trennung zur Laufzeit.

Positiv an der Laufzeittrennung ist die Option der Mehrsprachigkeit / Mehr-'Runtime'-igkeit. Dafür benötige ich keine fachliche Trennung.

Positiv ist, dass die Implementierung der einzelnen Services unabhängig ist. Hier können jeweils individuell optimale Architekturen / Persistenzstrategien u.ä. gewählt werden.

Negativ ist, dass für einen Austausch zwischen fachlichen Komponenten zwingend Nachrichtenverkehr erforderlich wird, dass ich verteilte Systeme qua default mitdenken muss. Viele Anfragen über fachliche Grenzen hinweg würden sich ohne permanenten Bezug zu einer mit physischem Zustand behafteten Deploymentkomponente beantworten lassen. Doch diese Option passt nicht mehr in den Microservice-Zuschnitt.

Negativ ist die Fixierung auf (reinen) Datenaustausch für fachliche Kommunikation. Dies konterkariert vieles, was mit Domain Driven Design und CQRS in den letzten 10 Jahren erarbeitet wurde. Besonders im Rahmen der REST/HTTP Fixierung bringt die Verheissung des leicht zu wartenden Microservice eine Rückverlagerung des Fokusses des Softwaredesigns von Verben auf Substantive mit sich.

Warum sind Microservices so verlockend? Ich denke, es sind primär diese Eigenschaften: 'Kleine funktionale Einheiten' 'unabhängige Ausführung' 'Kommunikation durch Nachrichtenaustausch' 'Asynchronität' 'Kapselung fachlichen Verhaltens'. Kommt's bekannt vor? 

Richtig, das ist einer der ältesten Definition von Objektorientierung. Smalltalk und Alan Kay lassen grüßen. Ja, entlang dieser Leitlinien gebaute Software ist besser verständlich, besser wartbar. Dazu benötige ich aber keine physisch getrennten Prozesse, die sowohl im Betrieb (Monitoring, Deployment, Kompatibilität) als auch unter dem Verteilte Systeme Aspekt Herausforderungen mit sich bringen.

Und wenn tatsächlich der Betrieb von phyisch verteilten/getrennten Komponenten attraktiv ist? Dann würde ich das aBC Konzept von Udi Dahan ins Feld führen. Dessen "autonome fachliche Komponenten" sind auch Zuschnitte entlang fachlicher Grenzen. Allerdings können Sie verschieden Tiers enthalten. Deren Kommunikation wird nun aber zu einem Implementierungsdetail. Die tatsächlich Integration von verschiedenen Komponenten geschieht durch fachlich motivierte, an CQ(R)S ausgerichtete Schnittstellen. Ob eine Anfrage lokal im physischen Bereich des Aufrufers beantwortet werden kann oder ob ein Rückgriff auf eine andere physische Verteilungseeinheit notwendig ist, liegt im Ermessen der Komponenten bzw. ihres Autors. Auch bei diesem Komponenten Ansatz kann die tatsächliche Implementierung und Subarchitektur je Komponente individuell gewählt werden. Manche Komponenten enthalten mehrere Tiers. Manche bestehen nur aus einer lokalen Komponente ("Dienst" im Sinne des taktischen DDD). Und manche .... bestehen nur aus einen entfernten Dienst - dieser ist äquivalent zu einem Microservice, der sich hier als Grenzfall einer degenerierten Komponente wiederfindet.

So sehe ich die aktuelle Microservice-Bewegung aus vielleicht etwas anderem Blickwinkel auch kritisch. Wo liegt dann der Einsatzzweck für das doch-nicht-Universalwerkzeug Microservice? Mindestens dort, wo ich evtl. sogar vorher existierende fachlich getrennte und polyglotte Teilsysteme verbinden muss. Dort werden Microservices sich der Herausforderung stellen müssen, ihre Schnittstellen universal zu definieren... Wie wärs mit XML, gar WDSL? Vielleicht erfinden wir nach OO und Komponenten auch SOA gleich noch mal neu...
