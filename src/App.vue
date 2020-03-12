<template>
    <div id="app">
        <vl-region>
            <vl-layout>
                <vl-introduction>
                    Dit standaardenregister geeft een overzicht van alle lopende en afgewerkte trajecten die deel
                    uitmaken van het
                    initiatief Open Standaarden voor Linkende Organisaties (OSLO) van de Vlaamse overheid.
                </vl-introduction>
            </vl-layout>
        </vl-region>
        <vl-region>
            <vl-layout>
                <p>Overheden op lokaal, Vlaams, interfederaal en Europees niveau moeten in het kader van hun
                    dienstverlening vaak samenwerken. In praktijk moeten bijgevolg heel wat gegevens uitgewisseld worden
                    tussen de verschillende administraties. Deze gegevens zijn afkomstig uit verschillende systemen,
                    zijn mogelijks niet in
                    hetzelfde technische formaat beschikbaar, en volgen niet noodzakelijk dezelfde semantiek. Zonder het
                    maken van afspraken,
                    wordt kwaliteitsvolle gegevensuitwisseling onmogelijk. Dit onderstreept het belang van de
                    ontwikkeling van datastandaarden.
                    De verschillende standaarden kunnen onderverdeeld worden op basis van waar ze zich bevinden in de
                    levenscyclus, namelijk:
                </p>
            </vl-layout>
        </vl-region>
        <vl-region>
            <vl-layout>
                <ul>
                    <li><strong>Erkende standaarden</strong>: werden na het doorlopen van een erkenningsprocedure
                        goedgekeurd door de Werkgroep Datastandaarden van het Stuurorgaan Vlaams Informatie- en
                        ICT-beleid als standaard binnen de Vlaamse overheid.
                    </li>
                    <li><strong>Kandidaat-standaarden</strong>: een stabiele specificatie voor de standaard werd
                        ontwikkeld, aan de hand van een publieke reviewperiode wordt implementatie-ervaring opgedaan en
                        feedback van buiten de thematische werkgroep verzameld.
                    </li>
                    <li><strong>Standaarden in ontwikkeling</strong>: werden reeds aangemeld bij de Werkgroep
                        Datastandaarden en worden uitgewerkt door een thematische werkgroep aan de hand van publieke
                        werksessies.
                    </li>
                </ul>
            </vl-layout>
        </vl-region>
        <vl-region>
            <vl-layout>
                <p>
                    Bij de ontwikkeling van een datastandaard is het van belang om de verschillende stakeholders te
                    aligneren, ook binnen de hiërarchie
                    van een organisatie. Om dit draagvlak bij de verschillende belanghebbenden te kunnen garanderen, is
                    vanuit OSLO een
                    <a href="https://data.vlaanderen.be/cms/Proces_en_methode_voor_de_erkenning_van_datastandaarden_v1.0.pdf">ontwikkelproces</a>
                    uiteengezet, gebaseerd op internationale best practices zoals onder meer ISA, W3C en OpenStand.
                    Het proces en de methode zijn geënt op principes van openheid en transparantie, het stimuleren van
                    hoge betrokkenheid,
                    en het bieden van de nodige garanties op vlak van stabiliteit, kwaliteit en toepasbaarheid.
                    Bovendien bestaan standaarden in een wijzigende omgeving, en dient er dus ruimte te zijn voor
                    beheerde wijzigingen en onderhoud van de
                    afspraken en standaarden.
                </p>
            </vl-layout>
        </vl-region>

        <vl-region>
            <vl-layout>
                <vl-title tag-name="h1">Erkende standaarden</vl-title>
                <div class="vl-u-table-overflow">
                    <vl-data-table mod-hover>
                        <thead>
                        <tr>
                            <th>Titel</th>
                            <th>Categorie</th>
                            <th>Verantwoordelijke organisatie</th>
                            <th>Type toepassing</th>
                            <th>Publicatiedatum</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="object in erkendeStandaarden">
                            <td>{{object.title}}</td>
                            <td>{{object.about}}</td>
                            <td><a :href=object.organisationID>{{object.organisation}}</a></td>
                            <td>{{object.usage}}</td>
                            <td>{{object.datePublished}}</td>
                        </tr>
                        </tbody>
                    </vl-data-table>
                </div>
            </vl-layout>
        </vl-region>


    </div>
</template>

<script>


    export default {
        name: 'App',
        data() {
            return {
                erkendeStandaarden: []
            }
        },
        methods: {
            async createErkendeStandaardenTable() {
                const erkendeStandaarden = require.context('../public/erkende-standaard-test');
                for (let index in erkendeStandaarden.keys()) {
                    const filePath = "http://localhost:8080/erkende-standaard-test" + erkendeStandaarden.keys()[index].substring(1, erkendeStandaarden.keys()[index].length);
                    const info = await this.extractData(filePath);
                    this.erkendeStandaarden.push(info);
                }
                console.log(this.erkendeStandaarden);
            },
            extractData(filePath) {
                return fetch(filePath).then(res => res.text()).then(html => {
                    const parser = new DOMParser();
                    const doc = parser.parseFromString(html, 'text/html');


                    let information = {};

                    const titles = doc.getElementsByTagName('h1');
                    for(let i = 0; i < titles.length ; i++){
                        const prop = titles[i].getAttribute('itemprop');
                        if(prop && prop === 'title'){
                            information['title'] = titles[i].innerHTML;
                        }
                    }

                    const divs = doc.getElementsByTagName('div');
                    for (let i = 0; i < divs.length; i++) {
                        const prop = divs[i].getAttribute('itemprop');
                        if (prop && prop != 'mainContentOfPage') {

                            const content = divs[i].innerHTML;
                            if (prop === 'publisher') {
                                const hrefs = divs[i].getElementsByTagName('a');
                                information.organisation = hrefs[0].text;
                                information.organisationID = hrefs[0].href;
                            } else {
                                information[prop] = divs[i].innerHTML;
                            }
                        }
                    }
                    return information;
                });
            }
        },
        mounted() {
            this.createErkendeStandaardenTable();
        }
    }
</script>

<style lang="scss">
    $vl-icon-font-location: "assets/";
    @import "~@govflanders/vl-ui-core/src/scss/core";
    @import "~@govflanders/vl-ui-content-header/src/scss/content-header";
    @import "~@govflanders/vl-ui-introduction/src/scss/introduction";
    @import "~@govflanders/vl-ui-data-table/src/scss/data-table";
    @import "~@govflanders/vl-ui-titles/src/scss/titles";
</style>