<script lang="ts">
  const month = new Date().getMonth() + 1;
  const day = new Date().getDate();
  const year = new Date().getFullYear();
  const thisYearBirthday = new Date(`11/01/${year}`);
  const today = new Date();

  const targetBirthday =
    thisYearBirthday > today ? thisYearBirthday : new Date(`11/01/${year + 1}`);
  const targetDateTime = targetBirthday.getTime();

  // Reactive variables
  let days = 0;
  let hours = 0;
  let minutes = 0;
  let seconds = 0;

  const countDown = setInterval(() => {
    const now = new Date().getTime();
    const distance = targetDateTime - now;

    days = Math.floor(distance / (1000 * 60 * 60 * 24));
    hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    seconds = Math.floor((distance % (1000 * 60)) / 1000);

    if (distance < 0) {
      clearInterval(countDown);
    }
  }, 1000);

  // Is it tomorrow?
  let tomorrowIsTheDay = false;
  if (month === 10 && day == 31) {
    tomorrowIsTheDay = true;
  }

  // Is it today?
  let todayIsTheDay = false;
  if (month === 11 && day == 1) {
    todayIsTheDay = true;
  }

  // Was it yesterday?
  let yesterdayWasTheDay = false;
  if (month === 11 && day == 2) {
    yesterdayWasTheDay = true;
  }
</script>

<main>
  <h1>Birthday for Conrad</h1>
  {#if tomorrowIsTheDay}<p>It's tomorrow 🤞</p>{/if}
  {#if todayIsTheDay}<p>It's today 🎉</p>{/if}
  {#if yesterdayWasTheDay}<p>It was yesterday 🎉</p>{/if}
  {#if !todayIsTheDay && !yesterdayWasTheDay}<p>
      <span>Wish me a happy birthday in: </span>
      <span>{days}</span> days
      <span>{hours}</span> hours
      <span>{minutes}</span> minutes
      <span>{seconds}</span> seconds
    </p>{/if}
</main>
