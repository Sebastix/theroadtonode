## Thunderhub updaten

Stop de Thunderhub service  
`sudo systemctl stop thunderhub`

Ga naar de applicatie directory  
`cd ~/thunderhub`

Update de repository met de laatste wijzigingen via Git:  
`git fetch --all`

Toon de laatste versie / tag
```bash
git describe --tags `git rev-list --tags --max-count=1`
```

Haal de wijzigingen op van de laatste versie  
`git checkout <output van vorige stap> #bijvoorbeeld v0.12.4`

Installeer de software
```bash 
npm install
npm run build
```

Start de Thunderhub service  
`sudo systemctl start thunderhub`

Thunderhub is nu bijgewerkt!