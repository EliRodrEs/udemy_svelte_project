<script>
  import Header from "./UI/Header.svelte"
  import MeetupGrid from "./Meetups/MeetupGrid.svelte"
  import TextInput from "./UI/TextInput.svelte"
  import Button from "./UI/Button.svelte"

  let title = ''
  let subtitle = ''
  let address = ''
  let description = ''
  let imageUrl = ''
  let email = ''

  let meetups = [
    {
      id: 'm1',
      title: 'Coding Bootcamp',
      subtitle: 'Learn to code in 2 hours',
      description: 'In this meetup, we will have some experts that teach you how to code!',
      imageUrl: 'https://evelongames.com/wp-content/uploads/2022/04/MaleniaEspadaMiquella.jpg',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'code@test.com'
    },
    {
      id: 'm2',
      title: 'Swim Together',
      subtitle: 'Let\'s go for some swimming',
      description: 'We will simply swim some rounds!',
      imageUrl: 'https://gcdn.lanetaneta.com/wp-content/uploads/2022/03/Elden-Ring-Quien-es-la-reina-Marika-segun-Lore.jpg',
      address: '27th Nerd Road, 32523 New York',
      contactEmail: 'swim@test.com'
    }
  ]

  function addMeetup(){
    const newMeetup = {
      id: Math.random().toString(),
      title: title,
      subtitle: subtitle,
      address: address,
      description: description,
      imageUrl: imageUrl,
      contactEmail: email
    }
    meetups = [...meetups, newMeetup] /* WE CAN CHANGE THE ORDER OF THIS ARRAY IF WE WANT THE LAST MEETUP TO APPEAR FIRST  [newMeetup, ...meetups] */
  }
</script>

<Header />

<main>
  <form on:submit|preventDefault={addMeetup}>

    <TextInput controlType="text" id="title" label="Title" value={title} on:input={event => (title = event.target.value)} />
    <TextInput controlType="text" id="subtitle" label="Subtitle" value={subtitle} on:input={event => (subtitle = event.target.value)} />
    <TextInput controlType="text" id="address" label="Address" value={address} on:input={event => (address = event.target.value)} />
    <TextInput controlType="text" id="imageUrl" label="Image URL" value={imageUrl} on:input={event => (imageUrl = event.target.value)} />
    <TextInput controlType="email" id="email" label="Email" value={email} on:input={event => (email = event.target.value)} />
    <TextInput id="description" controlType="textarea" rows="3" label="Description" value={description} on:input={event => (description = event.target.value)} />

    <Button type="submit" caption="Save" />
  </form>
  <MeetupGrid {meetups}/>
</main>

<style>
  main {
    margin-top: 7rem;
  }

  form {
    width: 30rem;
    max-width: 90%;
    margin: auto;
  }
</style>



