# Postgres-5
## Consultes 

1) Obtenir el nom de totes les assignatures classificades per ordre alfabètic.
   - select nom from Assignatura order by nom;
2) 
   a) Obtenir les ciutats dels alumnes majors de 18 anys.
    - select ciutat from alumne where edat >18;

   b) El mateix però sense tuples (registres) repetides
    - select DISTINCT ciutat from alumne where edat >=18;
    
3) Extreure totes les dades de l'assignatura amb nom 'LABOSOFT'
   - select * from assignatura where nom LIKE 'LABOSOFT';
4) Obtenir els noms i l'edat dels alumnes que són de Lleida per ordre alfabètic (segons el
camp nom).
   - select nom,edat from alumne where ciutat like 'Lleida' order by nom;
   
5) Si fem la següent consulta ens dona error, perquè?:
SELECT nom, numalumnes FROM assignatura ORDER BY 3;

- Perquè l'order by tres no significa res
   
6) Obtenir el llistat de tots els alumnes majors d’edat (igual o major que de 18 anys),
classificant-los per la ciutat d'origen en ordre creixent i per la seva edat en ordre decreixent
dins dels de la mateixa ciutat.
   - select * from alumne where edat>=18 order by ciutat ASC,edat DESC;
  
 7) El mateix però volem que enlloc de nom, ens surti IDENTITAT, i enlloc de ciutat que ens
surti ORIGEN.
     - select nom as IDENTITAT,ciutat as ORIGEN from alumne where edat>=18 order by ciutat ASC,edat DESC;
  8) Suposem ara que volem saber el nom, l’edat i l’any de naixement de cada alumne. Ordeneu
la sortida per l'any de naixement en ordre decreixent.
      - select NOM,EDAT,(EXTRACT(YEAR FROM CURRENT_DATE)-edat) as any_naixement from alumne order by any_naixement DESC;
  9) Trobeu les assignatures que tenen com a mínim 20 alumnes menys que 'EDI'. Ordeneu el
resultat alfabèticament per nom de l'assignatura.
      - select * from assignatura where (select numalumnes from assignatura where nom like 'EDI')-20<numalumnes order by nom;
  10) Suposem ara que inserim el següent alumne(Observeu que el camp edat no s'omple, per tant tindrà valor nul):
    INSERT INTO Alumne (nom, ciutat) VALUES('Pere', 'Tremp');<br>

        a) Trobar el nom dels alumnes que no tenen edat. Ordeneu el resultat pel camp nom.<br>
               -  select nom from alumne where edat is null order by nom;<br>
        b) Trobeu ara els noms dels alumnes que si que tenen edat.<br>
              -  select nom from alumne where edat is not null order by nom;
