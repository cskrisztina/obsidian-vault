  

proj környezet basic auth: nn-7-4 zglLMQVB7q

nn form:[https://nn-7-4.dev.webtown.cloud/form-test](https://nn-7-4.dev.webtown.cloud/form-test)

n téma:

Az nn témák kapcsán egy kis apróság, hogy az nn-unbranded-theme, egy örököltetett téma, azaz minden ugyanaz benne mint a sima nn-theme-ben, kivéve pár dolgot, ami felül van benne írva! Ebből kifolyólag, gyakorlatilag érdemes mindig átadni mindkettőt, viszont az nn-unbranded-theme-et én mindig így buildelem (elvileg felesleges) de azóta nem volt gond, hogy valami nem stimmel az unbranded témás oldalakon:

HA nincs gulp: npm install -g gulp

node 16.13al lehet buildelni

  

1. cd nn-theme mappába

  

2. ott terminálban futtáss: `npm link`

  

3. cd az nn-unbranded-theme mappába

  

4. ott `gulp extend`

  

5. Válaszd ki a `Base theme`-t  és nyomj enter-t

  

6. Válaszd ki a `Search globally installed npm modules`-t, nyomj enter-t

  

7. Válaszd ki az `nn-theme`-t, nyomj enter-t

  

8. gulp build

  

  

email templatek helye:(portal.extbe kell felvenni)

[nn.email.templates.dir=](http://nn.email.templates.dir=)${liferay.home}/data/dependencies/email_templates/

Cloudra scp,aztán expertet megkérni hogy másolj fel a helyére

scp email_tempaltes.zip webtown@wtcloud100:/home/webtown/nn_data/email_templates

  

**DOkumentáció,release adás:**

- release esetén “impact analysis” és “runbook” minden esetben kell, a többi dokumentáció opcionális
    

- ezek általában az új release első elkészült feladata során kerülnek “létrehozásra” a megfelelő release mappában
    

- release adás során az átadásra kerülő modulok/téma/layout… md5 hashelésre kerül és ezek az azonosítók a runbook-ba bekerülnek
    

- javasolt hogy előbb össze szedni minden telepítő fájlt és az “md5sum * > checklist.chk” parancsal az össze telepítőre legenerálja az azonosítót és a checklist fájlban össze is gyűjti
    

- a release csomag esetén a gyökér mappában találhatóak az adott release dokumentumai, a telepítő állományok vagy sablon/struktúrák a /dependencies mappá kerülnek a megfelelő mappába (mint a repository-ban is, azaz modules, themes, layouttpl stb.)
    

- a release csomag feltöltése::filezilla:
    
    host:project6.webtown.hu
    
    username:nn
    
    jelszó:Ld1hYovHzltKb4
    
    port:2222
    

    ![[Screenshot from 2026-04-22 15-32-35.png]]
      
    
      
    
    kerül a project szerverre is (ssh [liferay@project.webtown.hu](mailto:liferay@project.webtown.hu)) a /home/sftp/nn/download/nn_release_dxp alá az alábbi név konvencióval Release_v_X_X_X_ÉÉÉÉ_HH_NN, ez alá az előző pontban tárgyalt struktúrában
    
-   
    

- a release dokumentáció feltöltésre kerül a az adott release scrum mate issue-jához
    
- a telepítő állomány az adott release drive mappájába is feltöltésre kerül
    
- nn-unbranded-theme esetén volt probléma hogy a leszármaztatott téma ne mvette fel az ős új szabályait ezért bevett szokás lett hogy mindig behúzzok azt:
    

- 1. cd nn-theme mappába
    
- 2. ott terminálban futtáss: npm link
    
- 3. cd az nn-unbranded-theme mappába
    
- 4. ott gulp extend
    
- 5. Válaszd ki a Base theme-t  és nyomj enter-t
    
- 6. Válaszd ki a Search globally installed npm modules-t, nyomj enter-t
    
- 7. Válaszd ki az nn-theme-t, nyomj enter-t
    
- 8. nn-unbranded-theme gulp build
    

  

  

Ha már meglévő releashez megy javítás akkor nem kell új dokumentáció csak a meglévőeket kell /kiegészíteni hash-t cserélni.

és sftpre is csak azt kell feltölteni ami változott