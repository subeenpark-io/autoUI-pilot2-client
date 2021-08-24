<script>
  import { Link, navigate } from "svelte-routing";

  const handleSubmit = () => {
    console.log(name, email);

    let url = "http://3.37.217.167:8000/api/users/";

    let response = fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: name,
        email: email,
      }),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        return data;
      });

    navigate("/before", { replace: true });
  };

  let name;
  let email;
</script>

<div class="container">
  <div class="title">
    <h1>AutoUI</h1>
  </div>
  <div class="explanation">
    <h3 class="subtitle">About Project AutoUI & Goal of the Pilot Study</h3>
    <br />
    Project AutoUI aims to develop a system that can support usage of AI model results
    without additional background knowledge when specific model/input data are given.
    To achieve this goal, in this pilot study, we want to observe how does a result
    of a AI model affects in ways of people achieveing their goals.

    <h3 class="subtitle">Scenario of the Pilot Study</h3>
    <br />
    You will be given with a list of 10 students who are US graduate school applicants
    for this cycle. They have 6 months left until the application, so there is still
    a room for slight change in scores and research experiences. Assuming that you
    are a dean of the department, list up 3 students that you want to recommend for
    the overseas graduate school scholarship program.
  </div>

  <form on:submit|preventDefault={handleSubmit}>
    Name: <input type="text" placeholder="name" bind:value={name} required />
    <br />
    Email: <input type="text" placeholder="email" bind:value={email} required />
    <br />
    <button class="next__btn" type="submit">Next</button>
  </form>

  <!-- <Link to="blog">Blog</Link><br />
  <Link to="about">About</Link> -->
</div>

<style>
  .container {
    width: 70%;
    height: 70%;
    padding: 20px;
    border-radius: 8px;
    border: 1px solid black;
    background-color: var(--lightGray-background);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .title {
    width: 100%;
    text-align: center;
    height: 20%;
  }

  .explanation {
    width: 100%;
    text-align: justify;
    font-size: 20px;
    display: flex;
    flex-direction: column;
  }

  .subtitle {
    width: 100%;
    text-align: left;
  }

  .next__btn {
    width: 100%;
  }

  h3 {
    margin: 20px 0 0 0;
  }
</style>
