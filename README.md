 Dokumentation för inlämningsuppgiften

Steg 1: Klona projektet och testa lokalt
1. Jag kopierade GitHub-länken till projektet: https://github.com/Degendeg/cua24s_gamestore.git
2. I Visual Studio valde jag “Clone a repository och klistrade in länken.
3. startade programet för att se om fungerade. det funka.

Steg 2: Ladda upp projektet till egen GitHub-repo
1. Jag skapade ett nytt repository på mitt GitHub-konto med namnet gamestore.
2. Jag använde terminalen för att skriva Git, koppla till origin och sedan pusha.
3. se koden nedan.
 
   git init
   git remote add origin https://github.com/gurdip6/gamestore.git
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   

Steg 3: Skapa Azure App Service
1. I Azure Portal valde jag Web App.
2. Jag satte namn: gamestore, valde .NET 8, region: North Europe och prisnivå B1.
3. Region sweden central lät mig inte ändra price plan. så fick välja North Europe
4. Jag aktiverade GitHub Continuous Deployment och kopplade till mitt repo gurdip6/gamestore på branch main.

Steg 4: Skapa GitHub Actions workflow
Azure skapade automatiskt en .yml-fil för deployment i github/workflows/-mappen. Jag justerade den för att se till att den:
- Byggde projektet med dotnet build
- Publicerade med dotnet publish
- Deployade till Azure via azure/webapps-deploy@v3

Steg 5: Konfigurera Managed Identity och federated credential
1. I Azure Portal gick jag till Managed Identities och valde min app gamestore-id.
2. Under Federated Credentials klickade jag på Add federated credential och fyllde i:
- Organisation: gurdip6
- Repository: gamestore
- Entity: Branch, namn: main
- Namn: github-actions
3. Detta gjorde det möjligt för GitHub att autentisera sig mot Azure utan hemligheter.

Steg 6: Sätt GitHub Secrets
1. Jag hade problem med att deploy så jag fick lägga till följande i GitHub under Settings > Secrets > Actions:
- AZUREAPPSERVICE_CLIENTID
- AZUREAPPSERVICE_TENANTID
- AZUREAPPSERVICE_SUBSCRIPTIONID

Värdena tog jag från Azure Portal under min Managed Identity.

Steg 7: Aktivera Application Insights
1. I Azure Portal gick jag till App Service > Application Insights.
2. Jag klickade Enable och kopplade gamestore.
3. Nu kan jag övervaka applikationens prestanda, få loggar, live metrics, fel och m.m

Steg 8: Aktivera HTTPS och grundläggande säkerhet i configuration
1. Aktiverade HTTPS Only.
2. Applikationen använder nu HTTPS som standard.

Steg 9: Verifiera deployment
1. Öppnade URL:  <a href="https://gamestore-dzedgdcph7h6chfe.northeurope-01.azurewebsites.net">gamestore-dzedgdcph7h6chfe.northeurope-01.azurewebsites.net</a>
2. Applikationen fungerade korrekt och kunde visa startsidan och andra vyer.

steg 10: Sammanfattning
- Webbapplikationen är nu publicerad på Azure App Service.
- Deployment sker automatiskt via GitHub Actions.
- Applikationen är säker (HTTPS) och övervakad (Application Insights).
- Allt är dokumenterat och du kan skapa allt det igen om du följer stegen ovan.

