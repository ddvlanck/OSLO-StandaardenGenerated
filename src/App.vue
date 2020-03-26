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
                <vl-grid class="vl-grid--align-center" mod-stacked>
                    <vl-column width="3">
                        <div class="vl-infotext-wrapper">
                            <div class="vl-infotext vl-infotext--badge">
                                <a href="#erkendeStandaarden">
                                    <div class="vl-infotext__value" data-vl-infotext-value>
                                        {{this.erkendeStandaarden.length}}
                                    </div>
                                    <div class="vl-infotext__text">erkende standaarden</div>
                                </a>
                            </div>
                        </div>
                    </vl-column>
                    <vl-column width="3">
                        <div class="vl-infotext-wrapper">
                            <div class="vl-infotext vl-infotext--badge">
                                <a href="#kandidaatStandaarden">
                                    <div class="vl-infotext__value" data-vl-infotext-value>
                                        {{this.kandidaatStandaarden.length}}
                                    </div>
                                    <div class="vl-infotext__text">kandidaat standaarden</div>
                                </a>
                            </div>
                        </div>
                    </vl-column>
                    <vl-column width="3">
                        <div class="vl-infotext-wrapper">
                            <div class="vl-infotext vl-infotext--badge">
                                <a href="#standaardenInOntwikkeling">
                                    <div class="vl-infotext__value" data-vl-infotext-value>
                                        {{this.standaardInOntwikkeling.length}}
                                    </div>
                                    <div class="vl-infotext__text">standaarden in ontwikkeling</div>
                                </a>
                            </div>
                        </div>
                    </vl-column>
                </vl-grid>
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
                <vl-dropdown-navigation label="Filter standaarden">
                    <vl-link-list>
                        <vl-link-list-item>
                            <vl-link @click="filterTables('All')" mod-block>
                                Alle standaarden
                            </vl-link>
                        </vl-link-list-item>
                        <vl-link-list-item>
                            <!-- Only applicatieprofielen because value to check contains &amp;-->
                            <vl-link @click="filterTables('applicatieprofielen')" mod-block>
                                Vocabularia & applicatieprofielen
                            </vl-link>
                        </vl-link-list-item>
                        <vl-link-list-item>
                            <vl-link @click="filterTables('Technische standaard')" mod-block>
                                Technische standaarden
                            </vl-link>
                        </vl-link-list-item>
                        <vl-link-list-item>
                            <vl-link @click="filterTables('Standaard voor organisatorische interoperabiliteit')"
                                     mod-block>
                                Standaarden voor organisatorische interoperabiliteit
                            </vl-link>
                        </vl-link-list-item>
                    </vl-link-list>
                </vl-dropdown-navigation>
            </vl-layout>
        </vl-region>


        <vl-region>
            <vl-layout>
                <vl-title id="erkendeStandaarden" tag-name="h1">Erkende standaarden</vl-title>
                <div v-if="!erkendError" class="vl-u-table-overflow">
                    <vl-data-table id="erkendeStandaardenTable" mod-hover>
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
                            <td><a :href="/erkende-standaard/ + object.path">{{object.title}}</a></td>
                            <td v-if="object.about.indexOf('&amp;') >= 0">
                                {{object.about.replace('amp;', '')}}
                            </td>
                            <td v-else>{{object.about}}</td>
                            <td><a :href=object.organisationID>{{object.organisation}}</a></td>
                            <td>{{object.type}}</td>
                            <td>{{object.datePublished}}</td>
                        </tr>
                        </tbody>
                    </vl-data-table>
                </div>
                <div v-else>
                    <vl-title tag-name="h5">Er zijn op dit moment geen erkende standaarden</vl-title>
                </div>
            </vl-layout>
        </vl-region>

        <vl-region>
            <vl-layout>
                <vl-title id="kandidaatStandaarden" tag-name="h1">Kandidaat standaarden</vl-title>
                <div v-if="!kandidaatError" class="vl-u-table-overflow">
                    <vl-data-table id="kandidaatStandaardenTable" mod-hover>
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
                        <tr v-for="object in kandidaatStandaarden">
                            <td><a :href="/kandidaat-standaard/ + object.path">{{object.title}}</a></td>
                            <td v-if="object.about.indexOf('&amp;') >= 0">
                                {{object.about.replace('amp;', '')}}
                            </td>
                            <td v-else>{{object.about}}</td>
                            <td><a :href=object.organisationID>{{object.organisation}}</a></td>
                            <td>{{object.type}}</td>
                            <td>{{object.datePublished}}</td>
                        </tr>
                        </tbody>
                    </vl-data-table>
                </div>
                <div v-else>
                    <vl-title tag-name="h5">Er zijn op dit moment geen kandidaat standaarden</vl-title>
                </div>
            </vl-layout>
        </vl-region>

        <vl-region>
            <vl-layout>
                <vl-title id="standaardenInOntwikkeling" tag-name="h1">Standaarden in ontwikkeling</vl-title>
                <div v-if="!ontwikkelingError" class="vl-u-table-overflow">
                    <vl-data-table id="ontwikkelingTable" mod-hover>
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
                        <tr v-for="object in standaardInOntwikkeling">
                            <td><a :href="/standaard-in-ontwikkeling/ + object.path">{{object.title}}</a></td>
                            <td v-if="object.about.indexOf('&amp;') >= 0">
                                {{object.about.replace('amp;', '')}}
                            </td>
                            <td v-else>{{object.about}}</td>
                            <td><a :href=object.organisationID>{{object.organisation}}</a></td>
                            <td>{{object.type}}</td>
                            <td>{{object.datePublished}}</td>
                        </tr>
                        </tbody>
                    </vl-data-table>
                </div>
                <div v-else>
                    <vl-title tag-name="h5">Er zijn op dit moment geen standaarden in ontwikkeling</vl-title>
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
                erkendeStandaarden: [],
                kandidaatStandaarden: [],
                standaardInOntwikkeling: [],
                erkendError: false,
                kandidaatError: false,
                ontwikkelingError: false
            }
        },
        methods: {
            filterTables(sortValue) {
                this.filterRows(sortValue, "erkendeStandaardenTable");
                this.filterRows(sortValue, "kandidaatStandaardenTable");
                this.filterRows(sortValue, "ontwikkelingTable");

            },
            filterRows(sortValue, tableID) {
                const table = document.getElementById(tableID);
                if (table) {
                    const rows = table.getElementsByTagName('tr');

                    if (sortValue === 'All') {
                        for (let i = 0; i < rows.length; i++) {
                            rows[i].style.display = "";
                        }
                    } else {
                        for (let i = 0; i < rows.length; i++) {
                            const td = rows[i].getElementsByTagName("td")[1];
                            if (td) {
                                let category = td.innerHTML;
                                if (category.indexOf(sortValue) < 0) {
                                    rows[i].style.display = "none";
                                } else {
                                    rows[i].style.display = "";
                                }
                            }
                        }
                    }
                }
            },
            init() {

                // Erkende standaarden
                try {
                    const erkendeStandaarden = require.context('../public/erkende-standaard');
                    if (erkendeStandaarden) {
                        this.erkendError = false;
                        this.createTable(erkendeStandaarden, 'erkende-standaard', this.erkendeStandaarden);
                    }
                } catch (e) {
                    this.erkendError = true;
                }

                // Kandidaat standaarden
                try {
                    const kandidaatStandaarden = require.context('../public/kandidaat-standaard');
                    if (kandidaatStandaarden) {
                        this.kandidaatError = false;
                        this.createTable(kandidaatStandaarden, 'kandidaat-standaard', this.kandidaatStandaarden);
                    }
                } catch (e) {
                    this.kandidaatError = true;
                }

                // Standaarden in ontwikkeling
                try {
                    const inOntwikkeling = require.context('../public/standaard-in-ontwikkeling');
                    if (inOntwikkeling) {
                        this.ontwikkelingError = false;
                        this.createTable(inOntwikkeling, 'standaard-in-ontwikkeling', this.standaardInOntwikkeling);
                    }
                } catch (e) {
                    this.ontwikkelingError = true;
                }
            },
            async createTable(standaarden, type, tableArray) {
                for (let index in standaarden.keys()) {
                    const filePath = "http://localhost:8080/" + type + standaarden.keys()[index].substring(1, standaarden.keys()[index].length);
                    const info = await this.extractData(filePath);
                    info.path = standaarden.keys()[index].substring(2, standaarden.keys()[index].length);
                    tableArray.push(info);
                }
            },
            extractData(filePath) {
                return fetch(filePath).then(res => res.text()).then(html => {
                    const parser = new DOMParser();
                    const doc = parser.parseFromString(html, 'text/html');


                    let information = {};

                    const titles = doc.getElementsByTagName('h1');
                    for (let i = 0; i < titles.length; i++) {
                        const prop = titles[i].getAttribute('itemprop');
                        if (prop && prop === 'title') {
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
            },
        },
        mounted() {
            this.init();
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
    @import "~@govflanders/vl-ui-infotext/src/scss/infotext";
    @import "~@govflanders/vl-ui-dropdown-navigation/src/scss/dropdown-navigation";
    @import "~@govflanders/vl-ui-link/src/scss/link";
    @import "~@govflanders/vl-ui-link-list/src/scss/link-list";
    @import "~@govflanders/vl-ui-popover/src/scss/popover";
    @import "~@govflanders/vl-ui-util/src/scss/util";

    p, ul {
        font-size: 1.8rem;
    }

</style>
