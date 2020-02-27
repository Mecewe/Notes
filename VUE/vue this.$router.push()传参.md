##vue this.$router.push()传参

###1、params 传参

注意⚠️：patams传参 ，路径不能使用path 只能使用name,不然获取不到传的数据

this.$router.push({name: 'dispatch', params: {paicheNo: obj.paicheNo}})

取数据：this.$route.params.paicheNo

###2、query传参

this.$router.push({path: '/transport/dispatch', query: {paicheNo: obj.paicheNo}})

取数据：this.$route.query.paicheNo


