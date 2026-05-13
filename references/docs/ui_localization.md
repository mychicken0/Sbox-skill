 about

Localization

When displaying text such as Hello World , you should instead use a localization token like

#menu.helloworld . This will automatically replace the text with the corresponding language set by the user

when set on a Label, allowing you to easily support multiple languages.

Tokens

In UI, any displayed string that begins with a # will be recognized as a token, which means it will look for it's

real value in the localization system.

Example

Filename: Localization/en/sandbox.json

 "menu.helloworld": "Hello World",
 "spawnmenu.props": "Models",
 "spawnmenu.tools": "Tools"
 "spawnmenu.cloud": "sbox.game",

T hen it's as easy as doing the following:

<label>#spawnmenu.props</label>

Languages

Eng lis h Na me

A P I L a ng ua g e Co d e

Arabic

Bulgarian

Simplified Chinese

Traditional Chinese

Czech

ar

bg

zh-cn

zh-tw

cs

A P I L a ng ua g e Co d e

Danish

Dutch

English

Finnish

French

German

Greek

Hungarian

Italian

Japanese

Korean

Norwegian

Pirate

Polish

Portuguese

Portuguese-Brazil

Romanian

Russian

Spanish-Spain

Spanish-Latin America

Swedish

Thai

Turkish

Ukrainian

Vietnamese

da

nl

en

fi

fr

de

el

hu

it

ja

ko

no

en-pt

pl

pt

pt-br

ro

ru

es

es-419

sv

th

tr

uk

vn

Create d 24 Se p 2024

Updated 24 Se p 2024