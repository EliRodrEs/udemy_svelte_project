<script>
  import Header from "./UI/Header.svelte"
  import MeetupGrid from "./Meetups/MeetupGrid.svelte"
  import EditMeetup from './Meetups/EditMeetup.svelte'
  import Button from "./UI/Button.svelte"


  let meetups = [
    {
      id: 'm1',
      title: 'Coding Bootcamp',
      subtitle: 'Learn to code in 2 hours',
      description: 'In this meetup, we will have some experts that teach you how to code!',
      imageUrl: 'https://evelongames.com/wp-content/uploads/2022/04/MaleniaEspadaMiquella.jpg',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'code@test.com',
      isFavourite: false
    },
    {
      id: 'm2',
      title: 'Swim Together',
      subtitle: 'Let\'s go for some swimming',
      description: 'We will simply swim some rounds!',
      imageUrl: 'https://gcdn.lanetaneta.com/wp-content/uploads/2022/03/Elden-Ring-Quien-es-la-reina-Marika-segun-Lore.jpg',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'swim@test.com',
      isFavourite: false
    }
  ]

  let editMode

  function addMeetup(event){
    let {title, subtitle, address, description, imageUrl, email} = event.detail

    const newMeetup = {
      id: Math.random().toString(),
      title: title,
      subtitle: subtitle,
      address: address,
      description: description,
      imageUrl: imageUrl,
      contactEmail: email
    }
    meetups = [newMeetup, ...meetups] /* WE CAN CHANGE THE ORDER OF THIS ARRAY [...meetups, newMeetup] */
    editMode = null
  }

  function toggleFavourite(event){
    const id = event.detail
    const updatedMeetup = {...meetups.find(m => m.id === id)}
    updatedMeetup.isFavourite = !updatedMeetup.isFavourite
    const meetupIndex = meetups.findIndex(m => m.id === id)
    const updatedMeetups = [...meetups]
    updatedMeetups[meetupIndex] = updatedMeetup
    meetups = updatedMeetups
  }
</script>

<Header />

<main>
  <div class="meetup_controls">
    <Button caption="New Meetup" on:click={() => editMode = 'add'}/>
  </div>
  {#if editMode}
    <EditMeetup on:save={addMeetup}/>
  {/if}
  <MeetupGrid {meetups} on:toggle_favourite={toggleFavourite}/>
</main>

<style>
  main {
    margin-top: 7rem;
  }
  .meetup_controls {
    margin: 1rem;
  }
</style>



