# Dynamic DNS

{% hint style="info" %}
Tijd: 15 minuten
{% endhint %}

Je kunt je Bitcoin en Lightning node standaard alleen gebruiken vanaf hetzelfde netwerk. Met andere woorden: als jouw Raspberry Pi in je huis staat en met jouw router verbonden is, dan kan je hem alleen benaderen als jij ook thuis bent en met dezelfde router verbonden bent. Maar stel nou dat je niet thuis bent maar wel een betaling wil doen? Misschien wil je wel een biertje afrekenen met Lightning bij je favoriete cafe. Vrij onhandig als je eerst naar huis moet om af te rekenen, als de cafe eigenaar dat al toestaat. Of misschien wil je om andere redenen je node van buiten je thuisnetwerk aanroepen.

Als je van buiten je netwerk met de node wil communiceren, moet je huis een eigen IP-adres hebben. Het probleem is echter dat veel ISP's dynamische IP-adressen hanteren. Dat houdt in dat je huis zo nu en dan een nieuw IP-adres toegewezen krijgt. Bij de 1 gebeurt dat vaker dan bij de ander, maar dat het irritant kan zijn is zeker. Want stel dat je je biertje met Lightning wil afrekenen door gebruik te maken van je eigen node. Je app geeft een foutmelding met een tekst dat lijkt op "je node is onvindbaar". Dat komt omdat de app op jouw mobiel niet op de hoogte is van het nieuwe IP-adres van je huis. In plaats van af te rekenen met Lightning sta je borden af te wassen.

Gelukkig is het probleem te omzeilen. Er zijn tal van DDNS \(Dynamic DNS\) diensten online te vinden. Sommigen zijn zelfs gratis zoals [DuckDNS](https://www.duckdns.org/). In deze gids maken we gebruiken van [Google Domains](https://domains.google.com/). Velen van jullie zullen niet blij zijn met deze keuze, maar je staat vrij om aan de slag te gaan met een andere oplossing. Het fijne aan Google Domains is dat je heel gemakkelijk een ongelimiteerd aantal subdomeinen kunt aanmaken voor slechts €7,00 per jaar \(of hoe duur je domein is\). DuckDNS is weliswaar gratis, maar gelimiteerd tot 5 subdomeinen per account.

### Domeinnaam

Allereerst dien je een domeinnaam aan te schaffen via Google Domains. Je kunt zo goedkoop of duur gaan als je zelf wil. Een .de domein kost slechts €7,00 per jaar, maar voor een .finance domein ben je €57,00 per jaar kwijt. In deze guide gaan we er vanuit dat je voor "example.com" bent gegaan. Je zal het vaker zien terugkomen.



