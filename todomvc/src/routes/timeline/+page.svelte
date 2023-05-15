<script>
    import App3 from "../../components/App3.svelte";
    import Navbar from "../../components/Navbar.svelte";
    import ScrollyTeller from "../../components/ScrollyTeller.svelte";
</script>

<!-- <main>
    <a href="/frontpage">View Front Page</a>
</main> -->
<main>
<Navbar />

<App3 />
<ScrollyTeller />
</main>

<!-- <App3 /> -->

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->
<style>
    main {
        /* background-color: #efe9dd; */
        margin:0;
        padding:0;
    }

</style>