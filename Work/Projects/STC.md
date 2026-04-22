  

csapat laptop:borago /teamborago


local env/proj.környezet: Basic auth: stc-7-4 Mfqccao3elZREd031y8Q

[https://stc-7-4.dev.webtown.cloud](https://stc-7-4.dev.webtown.cloud/) [test@stc.org.sa](mailto:test@stc.org.sa) / test2

  

figma: [https://www.figma.com/design/0WtnmUrtT3qFw1tEsVmbo8/STC-Pay-Website-%E2%80%94-Hand-Off?node-id=443-51753&p=f&t=GzsBrmIYn9oahsLP-0](https://www.figma.com/design/0WtnmUrtT3qFw1tEsVmbo8/STC-Pay-Website-%E2%80%94-Hand-Off?node-id=443-51753&p=f&t=GzsBrmIYn9oahsLP-0)

march-stray-prior-silo

  

fragmenteknél:

`npm run build`

`npm run compress`

aztán buildben lévő zipet átmásolni a deployba


```
npm run build && npm run compress && cp build/liferay-fragments.zip /home/csombork/Develop/Liferay/bundles/stc-7.4-q1.5/deploy

```

  

Export/import:

  

Ezek alapján szerintem eleve egyszerűsíthetünk a content import forgatókönyvön: 0. Törlésre kerülnek a már telepített fragment entry collection-ök, illetve növelik az upload request size-ot 100MB-ről 1GB-re (600+MB a nagy LAR jelenleg).

1. Megtörténik a Site Nav expando-k importja és ezeken Guest view permission állítás.
    
2. Megtörténik a nagy Pages LAR import.
    
3. Megtörténik az Utility Page-ek importja (404, 500).
    
4. Importáljuk a language override-okat angolra és arabra külön-külön.    

  

 