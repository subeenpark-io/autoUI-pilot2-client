<script>
  import { Link, navigate } from "svelte-routing";

  let q1;
  let q2;
  let q3;

  const handleSubmit = () => {
    let url = "http://3.37.217.167:8000/api/feedbacks/";

    let response = fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        q1: q1,
        q2: q2,
        q3: q3,
      }),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        return data;
      });

    navigate("/thanks", { replace: true });
  };
</script>

<div class="container">
  <div class="title">
    <h1>AutoUI</h1>
  </div>
  <div class="explanation">
    <div class="survey question1">
      <h5 class="question question1">
        What actions did you perform to make your final decision?
      </h5>
      <textarea
        name=""
        id=""
        cols="30"
        rows="10"
        class="answer answer1"
        bind:value={q1}
      />
    </div>
    <div class="survey question2">
      <h5 class="question question2">
        Which UI components might help your action?
      </h5>
      <textarea
        name=""
        id=""
        cols="30"
        rows="10"
        class="answer answer2"
        bind:value={q2}
      />
    </div>
    <div class="survey question3">
      <h5 class="question question3">
        Please design your own page for the process that you performed right
        before.
      </h5>
      <textarea
        name=""
        id=""
        cols="30"
        rows="10"
        class="answer answer3"
        bind:value={q3}
      />
    </div>
  </div>
  <div class="button">
    <form on:submit|preventDefault={handleSubmit}>
      <button class="next__btn" type="submit">Thank you!</button>
    </form>
  </div>

  <!-- <Link to="blog">Blog</Link><br />
    <Link to="about">About</Link> -->
</div>

<style>
  .container {
    width: 70%;
    height: 80%;
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
    height: 10%;
  }

  .explanation {
    width: 100%;
    text-align: justify;
    font-size: 20px;
    display: flex;
    flex-direction: column;
    height: 80%;
  }

  .survey {
    width: 100%;
    height: 30%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
  }

  .question {
    width: 100%;
    text-align: left;
  }

  textarea {
    width: 100%;
  }

  .button {
    height: 10%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  form {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .next__btn {
    width: 30%;
    margin-bottom: 20px;
  }

  h5 {
    margin: 15px 0 0 0;
  }
</style>
