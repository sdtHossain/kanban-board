<template>
  <div class="container">
    <header class="d-flex flex-wrap justify-content-center py-3 mb-4 border-bottom">
      <a
        href="/"
        class="d-flex align-items-center mb-3 mb-md-0 me-md-auto link-body-emphasis text-decoration-none"
      >
        <svg class="bi me-2" width="40" height="32"><use xlink:href="#bootstrap"></use></svg>
        <span class="fs-4">Simple header</span>
      </a>

      <ul class="nav nav-pills">
        <li class="nav-item">
          <RouterLink to="/" class="nav-link active" aria-current="page">Home</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink :to="{ name: 'home' }" class="nav-link">Features</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink :to="{ name: 'home' }" class="nav-link">Pricing</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink :to="{ name: 'home' }" class="nav-link">FAQs</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink :to="{ name: 'about' }" class="nav-link">About</RouterLink>
        </li>
      </ul>
    </header>
  </div>
</template>
