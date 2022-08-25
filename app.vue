<template>
    <link rel="stylesheet" type="text/css" href="./css/flexboxgrid.min.css" media="screen" />
    <link rel="stylesheet" type="text/css" href="./css/main.css" media="screen" />
    <NuxtLayout >
        <NuxtPage />
    </NuxtLayout>
</template>

<script > 
export default {
    data() {
        return {
            
        }
    },
    head: {
        htmlAttrs: {
            lang: 'pt-br'
        },
        title: 'ISC - Instrutores',
        meta: [{ charset: 'utf-8' }, { name: 'viewport', content: 'width=device-width, initial-scale=1' }, { hid: 'description', name: 'description', content: 'Credenciamento' }],
        link: [{ rel: 'icon', type: 'image/x-icon', href: './favicon.ico' }]
    }
}
</script> 
