<template>
    <div class="bg-geral">
        <SiteHero />
        <SiteBenefits />
        <SiteHowWorks />
        <SiteAboutUs />
        <SiteStatistics />
        <SiteContact />               
    </div>
</template>

<script>

export default {
    layout: "site",
    data() {
        return {};
    },    
}
</script> 

<style lang="scss" scoped>
.bg-geral {
    .inner {
        max-width: 400px;
        color: green;
    }
}
</style>