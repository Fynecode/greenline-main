<script setup>
import { ref, onMounted } from 'vue'
import { Motion, inView } from '@oku-ui/motion'
import { Clock, Coins, Handshake } from 'lucide-vue-next'

// Refs to sections
const trust = ref(null)
const speed = ref(null)
const rates = ref(null)

// Animation visibility states
const trustVisible = ref(false)
const speedVisible = ref(false)
const rateVisible = ref(false)

onMounted(() => {
  // Activate inView only on the client (SSR-safe)
  if (trust.value) {
    inView(trust.value, ({ inView: v }) => {
      if (v) trustVisible.value = true
    })
  }

  if (speed.value) {
    inView(speed.value, ({ inView: v }) => {
      if (v) speedVisible.value = true
    })
  }

  if (rates.value) {
    inView(rates.value, ({ inView: v }) => {
      if (v) rateVisible.value = true
    })
  }

  // Inject JSON-LD metadata
  const script = document.createElement('script')
  script.type = 'application/ld+json'
  script.text = JSON.stringify({
    "@context": "https://schema.org",
    "@type": "Service",
    "serviceType": "Microloan Services",
    "provider": {
      "@type": "Organization",
      "name": "Greenline Financials",
      "url": "https://greenline-ubvx.onrender.com",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "15th Road 1393",
        "addressLocality": "Tsumeb",
        "addressCountry": "NA"
      },
      "email": "greenline@gmail.com",
      "telephone": "+264818669984"
    },
    "offers": {
      "@type": "OfferCatalog",
      "name": "Why Apply With Us",
      "itemListElement": [
        {
          "@type": "LoanOrCredit",
          "name": "Trusted Microloan Partner",
          "description": "Known for friendly support, transparency, and honest financial guidance."
        },
        {
          "@type": "LoanOrCredit",
          "name": "Quick Application Process",
          "description": "Fast approvals and simple requirements to help you move forward quicker."
        },
        {
          "@type": "LoanOrCredit",
          "name": "Affordable Low Rates",
          "description": "Fair and supportive interest rates built around your financial well-being."
        }
      ]
    }
  })
  document.head.appendChild(script)
})
</script>

<template>
  <section class="flex flex-col gap-16 text-primary">
    <h2 class="text-3xl lg:text-4xl font-bold leading-tight">
      Why apply with us?
    </h2>

    <div class="grid grid-rows-3 lg:grid-cols-3 md:grid-rows-1 w-full gap-5">

      <!-- TRUST -->
      <div ref="trust" class="flex flex-col gap-3 shadow-xl p-4 border border-primary rounded-lg bg-white">
        <Motion
          :initial="{ opacity: 0, y: 40 }"
          :animate="trustVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 40 }"
          :transition="{ duration: 0.7, ease: 'easeOut' }"
          :reducedMotion="false"
        >
          <Handshake :size="32" aria-hidden="true" class="text-accent" />
        </Motion>
        <div>
          <h3 class="max-sm:text-xl text-2xl font-bold">Trusted by the community</h3>
          <p class="text-lg">
            We keep things honest and transparent. Clients choose us because they know we’re here
            to make borrowing simple and stress-free.
          </p>
        </div>
      </div>

      <!-- SPEED -->
      <div ref="speed" class="flex flex-col gap-3 shadow-xl p-4 border border-primary rounded-lg bg-white">
        <Motion
          :initial="{ opacity: 0, y: 40 }"
          :animate="speedVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 40 }"
          :transition="{ duration: 0.7, ease: 'easeOut' }"
          :reducedMotion="false"
        >
          <Clock :size="32" aria-hidden="true" class="text-accent"/>
        </Motion>
        <div>
          <h3 class="max-sm:text-xl text-2xl font-bold">Fast and simple process</h3>
          <p class="text-lg">
            No long waits. No confusing steps. We review your application quickly so you can move
            forward sooner.
          </p>
        </div>
      </div>

      <!-- RATES -->
      <div ref="rates" class="flex flex-col gap-3 shadow-xl p-4 border border-primary rounded-lg bg-white">
        <Motion
          :initial="{ opacity: 0, y: 40 }"
          :animate="rateVisible ? { opacity: 1, y: 0 } : { opacity: 0, y: 40 }"
          :transition="{ duration: 0.7, ease: 'easeOut' }"
          :reducedMotion="false"
        >
          <Coins :size="32" aria-hidden="true" class="text-accent"/>
        </Motion>
        <div>
          <h3 class="max-sm:text-xl text-2xl font-bold">Fair, low rates</h3>
          <p class="text-lg">
            Our rates are designed to support your financial journey — not burden it.
          </p>
        </div>
      </div>

    </div>
  </section>
</template>
