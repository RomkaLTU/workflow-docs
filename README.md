!> Siųlomas workflow gali kisti priklausomai nuo projekto specifikos.

# Git

## Inicijuojama tuščia git repozitorija

```
git init
```

- Įsitikinam kad turime .gitignore su reikiamu turinu
- Komitinam

```
git add .
git commit -m "initial commit"
git remote add origin git@github.com:change/me.git
git push -u origin master
```

!> Command line naudojimas nėra būtinas, rekomanduojami šie GUI klientai: [GitTower](https://www.git-tower.com/), [GitKraken](https://www.gitkraken.com/)

## Darbas su branch'ais

- master - live versija, viskas kas bus pušinama į šį branch automatiškai keliaus į Live klientui
- release - naujos funkcijos išleidžiamos čia parodyti klientui, po patvirtinimo merginama į master
- develop - stabilus branchas, bet dar "neišreleasintas" pagrinde skirtas testuotojams. Po testavimo sumerginamas į develop

**Kiekvienas dev'as pradedamas darbą turėtu atsiskelti savo lokalią atšaką iš develop branch.**

# Deployment (CD)

?> Rekomenduojama naudoti [DeployHQ](https://www.deployhq.com/)

Nustačius projektą rezultate turėsime automatinį deploymentą pagal git brach'a.

Pvz.: pushinant į release, pakeitimai automatiškai sukris į staging (test) serverį.

!> Niekada nereikėtu tiesiogiai pushinti į master branchą, workflow visada yra **push to develop merge to -> release merge to -> master** Būna atveju kai yr areikalingas "hotfix" tuomet galima sukurti atskirą branch hotfix į kurį pushinant pakeitimai iškart bus merginami į master apeinant develop ir release.

# Staging, Live serveriai

Yra gera praktika, minimaliai turėti bent 1 staging (test) serverį į kurį kris pakeitimai iš release ir develop branchu.

?> Rekomenduojama naudoti [Forge](https://forge.laravel.com/)

Su forge galima lengvai tvarkytis su serveriais tiek live tiek staging, taip pat iš dalies jis glai atstoti ir DeployHQ servisą su tam tikrom išlygom. Forge tinka tiek Wordpress tiek Laravel Projektams.

Rekomenduotina susikurti wildcard subdomena kuris būtu nukreiptas į staging serverį pvz.: *.dev yra nukreiptas į serverį xx.xx.xx.xx tokių būdu galima dinamiškai kurtis projektus kaskart nelendant į DNS lentelę, nes **projectA.dev.expertmedia.lt** ir **projectB.dev.expertmedia.lt** ves į tą patį serverį tik skirtingus virtual host (atitinkamai sukonfiguruotus).

# Wordpress

?> Rekomenduojama naudoti [Bedrock](https://roots.io/bedrock/) ir [Sage](https://github.com/RomkaLTU/sage10-tailwindcss)

**Bedrock** - pakeista Wordpress failų struktūra, pridėtas composer. Naudojant Bedrock galime papraščiau tvarkytis su Wordpress projekto versijavimų. Visas funkcionalumas kuris buvo Wordpress išlieka nepakites. Taip pat yra papildomų naudingų dalykų kuriu nėra standartiškai Wordpress.

**Sage** - Wordpress temos "boilerplate". Naudojamas stackas:

- TailwindCSS
- PostCSS
- Laravel Blade
- Laravel

?> MacOS Valet naudojamas remomanduojama įsidiegti wp-cli ir jam skirtą pluginą [wp valet](https://github.com/aaemnnosttv/wp-cli-valet-command) kuris leis greitai kurti brojektus su komanda `wp valet project_name`

## Wordpress Plugins

?> Rekomanduojama naudoti WP plugin boilerplate [generatorių](https://wppb.me/)

Specifinis nestandartinis funkcionalumas turėtu būti kiek įmanoma dažniau permetamas į custom pluginus. Naudojant tokį boilerplate (kuris yra OOP principu padarytas) ateityje nebus problemų kažką pataisyti ir rasti kitiems programuotojams.

# Laravel

?> Rekomenduojamas [TALL](https://tallstack.dev/) stackas.

- **Tailwind CSS** - didelis produktyvumo pagerinimas, "kitas" būdas kodinti dizainus.
- **Alpine.js** - javascript funkcionalumas HTML'e idealiai tinka mažiems ir vidutiniams projektams, tam tikrus standartinius dalykus galima padaryti nerašant JS apskritai.
- **Livewire** - puikiai tinka su Alpine.js kombinacija galima išgauti taip vadinama "server side reactivity" taip pat nerašant JS, o pasikliaujant tik standartiniais Laravel metodais.

**TALL stack yra pilnai naudojamas projekte https://gostautoklinika.dev.hdd.lt**