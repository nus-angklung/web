<script>
    export let segment;
    const ensembleSubmenu = [
        { resource_path: 'about', display: 'About Us' },
        { resource_path: 'team', display: 'Team' },
    ];
    $: isInsideEnsembleSubmenu = ensembleSubmenu.some(
        (submenu) => submenu.resource_path === segment
    );
</script>

<style>
    :root {
        --highlight: #c4c4c4;
    }
    nav {
        font-size: 16px;
        font-weight: 500;
        z-index: 1;
    }
    .container {
        max-width: 80%;
        padding: 0 2em 2em;
        margin: 0 auto;
        box-sizing: border-box;
    }
    ul {
        display: flex;
        flex-direction: row;
        justify-content: flex-end;
        align-items: flex-end;
        list-style-type: none;
        padding-inline-start: unset;
    }
    li {
        display: block;
        text-align: center;
        padding: 5px;
    }
    li > * {
        box-sizing: border-box;
    }
    [aria-current] {
        position: relative;
        display: inline-block;
    }
    [aria-current]::after {
        position: absolute;
        content: '';
        width: calc(100% - 1em);
        height: 2px;
        background-color: var(--highlight);
        display: block;
        bottom: -1px;
    }
    a,
    span {
        text-decoration: none;
        padding: 0 0.5em 0.5em;
        display: block;
        width: 100%;
    }
    ul li > *:hover {
        opacity: 0.5;
    }
    .dropdown {
        display: flex;
        flex-direction: column;
    }
    .dropdown ul {
        transition: all 0.5s ease;
        margin-top: 1rem 5px 5px;
        background-color: transparent;
        text-align: center;
        opacity: 0;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .dropdown:hover > ul,
    .dropdown:hover > ul:hover {
        display: flex;
        opacity: 1;
        transform: translateY(calc(100% + 36px));
    }
    .dropdown ul li {
        clear: both;
        width: 100%;
    }
    .dropdown ul li a {
        box-sizing: border-box;
        text-align: center;
    }
    @media (max-width: 576px) {
        nav {
            font-size: 14px;
        }
        .container {
            max-width: 90%;
        }
    }
</style>

<nav class="container">
    <ul>
        <li>
            <a
                aria-current={segment === undefined ? 'page' : undefined}
                href=".">
                Home
            </a>
        </li>
        <li class="dropdown">
            <ul class="dropdown-content">
                {#each ensembleSubmenu as submenu}
                    <li>
                        <a href={submenu.resource_path}>{submenu.display}</a>
                    </li>
                {/each}
            </ul>
            <span aria-current={isInsideEnsembleSubmenu ? 'page' : undefined}>
                Our Ensemble
            </span>
        </li>
        <li>
            <a
                aria-current={segment === 'our-music' ? 'page' : undefined}
                href="our-music">
                Our Music
            </a>
        </li>
        <li>
            <a
                aria-current={segment === 'news' ? 'page' : undefined}
                href="news">
                News
            </a>
        </li>
        <li>
            <a
                aria-current={segment === 'contact' ? 'page' : undefined}
                href="contact">
                Contact Us
            </a>
        </li>
    </ul>
</nav>
