<template>
    <div>
        <div id="slogan" class="text-center">
            <h1>Pagina Principal</h1>
            <br />
            <h6 class="text-secondary">Gerador de nomes ultilizando Vue.Js, GraphQl e Node</h6>
        </div>
        <div id="main">
            <div class="container">
                <div class="row">
                    <div class="col-md">
                        <h5>
                            Prefixos
                            <span class="badge badge-info">{{prefixes.length}}</span>
                        </h5>
                        <div class="card">
                            <div class="card-body">
                                <ul class="list-group">
                                    <li
                                        class="list-group-item"
                                        v-for="prefixe in prefixes"
                                        v-bind:key="prefixe"
                                    >
                                        <div class="row">
                                            <div class="col-md">{{ prefixe }}</div>
                                            <div class="col-md text-right">
                                                <button
                                                    class="btn btn-info"
                                                    v-on:click="deletePrefix(prefix)"
                                                >
                                                    <span class="fa fa-trash"></span>
                                                </button>
                                            </div>
                                        </div>
                                    </li>
                                </ul>
                                <br />
                                <div class="input-group">
                                    <input
                                        class="form-control"
                                        type="text"
                                        v-model="prefix"
                                        v-on:keyup.enter="addPrefix(prefix)"
                                        placeholder="Digite o Prefixo"
                                    />
                                    <div class="input-group-append">
                                        <button class="btn btn-info" v-on:click="addPrefix(prefix)">
                                            <span class="fa fa-plus"></span>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-md">
                        <h5>
                            Sufixos
                            <span class="badge badge-info">{{ sufixes.length}}</span>
                        </h5>
                        <div class="card">
                            <div class="card-body">
                                <ul class="list-group">
                                    <li
                                        class="list-group-item"
                                        v-for="sufixe in sufixes"
                                        v-bind:key="sufixe"
                                    >
                                        <div class="row">
                                            <div class="col-md">{{ sufixe}}</div>
                                            <div class="col-md text-right">
                                                <button
                                                    class="btn btn-info"
                                                    v-on:click="deleteSufix(sufix)"
                                                >
                                                    <span class="fa fa-trash"></span>
                                                </button>
                                            </div>
                                        </div>
                                    </li>
                                </ul>
                                <br />
                                <div class="input-group">
                                    <input
                                        class="form-control"
                                        type="text"
                                        v-model="sufix"
                                        v-on:keyup.enter="addSufix(sufix)"
                                        placeholder="Digite o Sufixo"
                                    />
                                    <div class="input-group-append">
                                        <button class="btn btn-info" v-on:click="addSufix(sufix)">
                                            <span class="fa fa-plus"></span>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <br />
                <h5>
                    Dominios
                    <span class="badge badge-info">{{ domains.length}}</span>
                </h5>
                <div class="card">
                    <div class="card-body">
                        <ul class="list-group">
                            <li
                                class="list-group-item"
                                v-for="domain in domains"
                                v-bind:key="domain.name"
                            >
                                <div class="row">
                                    <div class="col-md text-size">{{ domain.name}}</div>
                                    <div class="col-md text-right">
                                        <a
                                            class="btn btn-info"
                                            v-bind:href="domain.checkout"
                                            target="_blank"
                                        >
                                            <span class="fa fa-shopping-cart"></span>
                                        </a>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
    name: "app",
    data() {
        return {
            prefix: "",
            sufix: "",
            prefixes: ["Air", "Vest"],
            sufixes: ["France", "Brazil"]
        };
    },
    methods: {
        addPrefix(prefix) {
            this.prefixes.push(prefix);
            this.prefix = "";
        },
        addSufix(sufix) {
            this.sufixes.push(sufix);
            this.sufix = "";
        },
        deletePrefix(prefix) {
            this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
        },
        deleteSufix(sufix) {
            this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
        }
    },
    computed: {
        domains() {
            const domains = [];
            for (const prefix of this.prefixes) {
                for (const sufix of this.sufixes) {
                    const name = prefix + sufix;
                    const url = name.toLowerCase();
                    const checkout =
                        "https://checkout.hostgator.com.br/?a=add&sld=" +
                        url +
                        "&tld=.org";
                    domains.push({ name, checkout });
                }
            }
            return domains;
        }
    }
};
</script>

<style>
#slogan {
    margin-top: 30px;
    margin-bottom: 30px;
}

#main {
    background-color: #c2bbbb;
    padding: 30px;
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
}
</style>
