<script lang="ts">
  import Button from "../lib/components/Button.svelte";
  import Carousel from "../lib/components/Carousel.svelte";

  let scrollY = 0;

  const venueImages = [
    {
      src: "/images/inn-drone-shot.png",
      alt: "The Waterford Inne - drone shot",
    },
    {
      src: "/images/inn-slideshow-2.png",
      alt: "The Waterford Inne",
    },
    {
      src: "/images/inn-slideshow-3.png",
      alt: "The Waterford Inne",
    },
    {
      src: "/images/inn-slideshow-4.png",
      alt: "The Waterford Inne",
    },
    {
      src: "/images/inn-slideshow-5.png",
      alt: "The Waterford Inne",
    },
  ];
</script>

<svelte:window on:scroll={() => (scrollY = window.scrollY)} />

<div>
  <div
    class="flex flex-col w-full mb-10 mt-16 max-w-[1200px] mx-auto px-5 lg:px-6"
  >
    <h1 class="lg:text-[120px] md:text-[90px] text-[65px] animate-fade-in">
      Nicole & Dan
    </h1>
    <!-- <p class="text-slate-600">September 26, 2026</p> -->
  </div>
  <!-- <div
      role="img"
      aria-label="Nicole & Dan"
      class="h-[60vh] w-full bg-fixed bg-cover bg-center bg-no-repeat"
      style="background-image: url('/images/inn-pic.png');"
    ></div> -->
  <div class="relative h-[72vh] w-full overflow-hidden">
    <img
      src="/images/inn-pic.png"
      alt="Nicole & Dan"
      class="absolute w-full object-cover will-change-transform"
      style={`height: calc(72vh + 400px); top: -230px; transform: translateY(${Math.min(scrollY * 0.5, 400)}px);`}
    />
  </div>
  <div
    class="relative z-[9999] -mt-24 flex flex-col text-center w-full mx-auto items-center justify-center px-5 lg:px-6 py-20 bg-white"
  >
    <div class="max-w-lg">
      <h2 class="">See you in Maine</h2>
      <img src="/images/maine-icon.png" alt="maine" class="w-8 mx-auto pb-5" />
      <h2 class="">09.26.26</h2>
      <p class=" text-lg">
        We're getting married in beautiful Waterford, Maine, just minutes away
        from Nicole's family cabin, and we'd love for you to join us. This
        website will have everything you need to know — from the ceremony
        schedule to where to stay.
      </p>

      <!-- <div class="h-[1px] bg-slate-200 w-full my-10"></div>
        <p class="text-slate-700 text-lg">September 26, 2026</p>
        <h3>The Waterford Inne</h3> -->
      <div class="h-[1px] bg-slate-200 w-full my-20"></div>
      <p class=" uppercase text-sm tracking-[0.08em]">The Venue</p>
      <h2 id="venue" class="scroll-mt-20">The Waterford Inne</h2>
      <p class=" text-lg">
        The Waterford Inne is an 1826 homestead turned farmhouse inn. It is
        located on seventeen peaceful acres of grounds, gardens, and woods.
      </p>
    </div>
    <Carousel images={venueImages} />
    <div
      class="w-full max-w-[1200px] mx-auto flex items-center justify-between mt-6"
    >
      <div class="text-left">
        <p>258 Chadbourne Rd</p>
        <p>Waterford, ME 04088</p>
      </div>
      <Button
        href="https://maps.app.goo.gl/XZFKj6163KWqdW5v7"
        label="Open in Maps"
        size="md"
        variant="solid"
        target="_blank"
      />
    </div>
    <div
      id="travel"
      class="w-full max-w-[1200px] mx-auto md:grid md:grid-cols-2 gap-10 my-32 items-center scroll-mt-20 flex flex-col-reverse"
    >
      <div class="text-left">
        <p class=" uppercase text-sm tracking-[0.08em]">Travel</p>
        <h2 class="">Where to Stay</h2>
        <p class="text-lg text-balance">
          We've asssembled some local lodging options. There are also still a
          variety of rentals available in the area.
        </p>
        <div class="h-[1px] bg-slate-200 w-full my-10"></div>

        <div class="flex items-center justify-between">
          <div class="space-y-2">
            <h3>Center Lovell Inn</h3>
            <p class="text-balance">
              Historic bed and breakfast, a 25-minute drive to the venue.
            </p>
          </div>
          <Button
            href="https://centerlovellinn.co/"
            label="Book Now"
            size="md"
            variant="solid"
            target="_blank"
          />
        </div>

        <div class="h-[1px] bg-slate-200 w-full my-10"></div>

        <div class="flex items-center justify-between">
          <div class="space-y-2">
            <h3>Hampton Inn Oxford</h3>
            <p class="text-balance">
              Enjoy views of the White Mountains from your room, a 25-minute
              drive to the venue.
            </p>
          </div>
          <Button
            href="https://www.hilton.com/en/hotels/pwmoxhx-hampton-oxford/"
            label="Book Now"
            size="md"
            variant="solid"
            target="_blank"
          />
        </div>
        <div class="h-[1px] bg-slate-200 w-full my-10"></div>
        <div class="flex items-center justify-between">
          <div class="space-y-2">
            <h3>Oxford Casino Hotel</h3>
            <p class="text-balance">
              Comfort and covenience in the heart of Oxford, a 25-minute drive
              to the venue.
            </p>
          </div>
          <Button
            href="https://www.oxfordcasino.com/"
            label="Book Now"
            size="md"
            variant="solid"
            target="_blank"
          />
        </div>
        <div class="h-[1px] bg-slate-200 w-full my-10"></div>
        <div class="flex items-center justify-between">
          <div class="space-y-2">
            <h3>Airbnb Rentals</h3>
            <p class="text-balance">
              This list of rentals are a great place to start for those looking
              for a more private experience. Please note that availability is
              subject to change.
            </p>
          </div>
          <Button
            href="https://www.airbnb.com/wishlists/viewonly/dcc5facd-c425-400d-86e8-6195c2c8eb49?s=67&unique_share_id=12463f4a-1ff8-4b99-8746-e08e8e124457"
            label="View List"
            size="md"
            variant="solid"
            target="_blank"
          />
        </div>
      </div>
      <img
        src="/images/where-to-stay.png"
        alt="airbnb cabin"
        class="w-full h-full object-cover mt-10 rounded-md"
      />
    </div>
    <div id="schedule" class="max-w-[1200px] mx-auto my-20 scroll-mt-20">
      <!-- <p class=" uppercase text-sm tracking-[0.08em]">Schedule</p> -->
      <h2 class="">Schedule</h2>
      <p class=" text-lg">
        We're still planning the day's events and will update this section soon.
      </p>
    </div>
    <div
      id="registry"
      class="w-full max-w-[1200px] mx-auto my-20 bg-slate-100 py-20 rounded-md scroll-mt-20"
    >
      <div class="max-w-lg mx-auto">
        <h2 class="">Registry</h2>
        <p class="text-lg text-balance pb-10">
          Sharing our wedding day with you is what matters most to us. If you
          would like to give a gift, you can find our registry below.
        </p>
        <Button
          href="https://www.zola.com/registry/nicoleanddanseptember26"
          label="View Registry"
          size="md"
          variant="solid"
          target="_blank"
        />
      </div>
    </div>
    <div id="things-to-do" class="max-w-xl mx-auto my-20 scroll-mt-20">
      <!-- <p class=" uppercase text-sm tracking-[0.08em]">Schedule</p> -->
      <h2 class="">Things To Do</h2>
      <p class="text-lg text-balance">
        We're making a list of activities and sights in the area. Maine is a
        great place to visit in the fall, so check back soon for our
        recommendations.
      </p>
    </div>
    <div class="h-[1px] bg-slate-200 w-full mx-auto my-10"></div>
    <div id="faq" class="max-w-xl mx-auto my-20 scroll-mt-20">
      <!-- <p class=" uppercase text-sm tracking-[0.08em]">Schedule</p> -->
      <h2 class="">FAQs</h2>
      <p class="text-lg text-balance">Hard at work on these... Stay tuned.</p>
    </div>
  </div>
</div>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&display=swap");
</style>
