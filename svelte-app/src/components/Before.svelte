<script>
  import { Link, navigate } from "svelte-routing";
  const handleSubmit = () => {
    console.log(candidates, reason);
    let url = "http://3.37.217.167:8000/api/befores/";

    let response = fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        candidates: candidatesString,
        reasons: reason,
      }),
    })
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        return data;
      });

    navigate("/after", { replace: true });
  };

  let reason;

  let candidates = [];

  $: candidatesString = candidates.join(" ");

  let array = [
    {
      id: 1,
      name: "최예은",
      gre: 331,
      toefl: 80,
      uni: 5,
      sop: 2.5,
      lor: 5.0,
      cgpa: 8.78,
      research: 0,
      probability: 0.7288,
    },
    {
      id: 2,
      name: "진정수",
      gre: 311,
      toefl: 90,
      uni: 5,
      sop: 0.5,
      lor: 2.5,
      cgpa: 7.76,
      research: 0,
      probability: 0.5144,
    },
    {
      id: 3,
      name: "황민지",
      gre: 324,
      toefl: 117,
      uni: 5,
      sop: 1.5,
      lor: 2.5,
      cgpa: 8.86,
      research: 1,
      probability: 0.7823,
    },
    {
      id: 4,
      name: "김중수",
      gre: 300,
      toefl: 82,
      uni: 5,
      sop: 4.0,
      lor: 1.5,
      cgpa: 8.65,
      research: 1,
      probability: 0.6619,
    },
    {
      id: 5,
      name: "김성수",
      gre: 318,
      toefl: 93,
      uni: 5,
      sop: 1.5,
      lor: 2.5,
      cgpa: 6.78,
      research: 1,
      probability: 0.5064,
    },
    {
      id: 6,
      name: "송명자",
      gre: 288,
      toefl: 109,
      uni: 5,
      sop: 4.0,
      lor: 5.0,
      cgpa: 6.84,
      research: 0,
      probability: 0.49,
    },
    {
      id: 7,
      name: "박예원",
      gre: 318,
      toefl: 90,
      uni: 5,
      sop: 1.0,
      lor: 2.5,
      cgpa: 6.81,
      research: 0,
      probability: 0.5008,
    },
    {
      id: 8,
      name: "김영일",
      gre: 306,
      toefl: 78,
      uni: 5,
      sop: 4.0,
      lor: 5.0,
      cgpa: 7.81,
      research: 0,
      probability: 0.4806,
    },
    {
      id: 9,
      name: "이영일",
      gre: 327,
      toefl: 109,
      uni: 5,
      sop: 3.5,
      lor: 2.0,
      cgpa: 9.54,
      research: 1,
      probability: 0.9011,
    },
    {
      id: 10,
      name: "이수민",
      gre: 320,
      toefl: 99,
      uni: 5,
      sop: 4.0,
      lor: 0.5,
      cgpa: 8.54,
      research: 1,
      probability: 0.7138,
    },
  ];

  let sortBy = { col: "id", ascending: true };

  $: sort = (column) => {
    if (sortBy.col == column) {
      sortBy.ascending = !sortBy.ascending;
    } else {
      sortBy.col = column;
      sortBy.ascending = true;
    }

    // Modifier to sorting function for ascending or descending
    let sortModifier = sortBy.ascending ? 1 : -1;

    let sort = (a, b) =>
      a[column] < b[column]
        ? -1 * sortModifier
        : a[column] > b[column]
        ? 1 * sortModifier
        : 0;

    array = array.sort(sort);
  };
</script>

<div class="container">
  <div class="table">
    <span>* You can sort colums by clicking the head of the colum.</span>
    <table>
      <thead>
        <tr>
          <th />
          <th on:click={sort("id")}>id</th>
          <th on:click={sort("name")}>name</th>
          <th on:click={sort("gre")}>GRE Score(340)</th>
          <th on:click={sort("toefl")}>TOEFL Score(120)</th>
          <th on:click={sort("cgpa")}>Cumulative GPA(10)</th>
          <th on:click={sort("research")}>Research Experience</th>
          <th on:click={sort("sop")}>Statement of Purpose(5)</th>
          <th on:click={sort("lor")}>Letter of Recommendation(5)</th>
        </tr>
      </thead>
      <tbody>
        {#each array as row}
          <tr>
            <td
              ><input
                type="checkbox"
                bind:group={candidates}
                name="candidates"
                value={row.name}
              /></td
            >
            <td>{row.id}</td>
            <td>{row.name}</td>
            <td>{row.gre}</td>
            <td>{row.toefl}</td>
            <td>{row.cgpa}</td>
            <td>{row.research == 1 ? "YES" : "NO"}</td>
            <td>{row.sop}</td>
            <td>{row.lor}</td>
          </tr>
        {/each}
      </tbody>
    </table>
    <div class="data-explanation">
      <ul>
        <li>GRE:</li>
        <li>TOEFL:</li>
        <li>Cumulative GPA:</li>
        <li>Research Experience:</li>
        <li>Statement of Purpose:</li>
        <li>Letter of Recommendation:</li>
      </ul>
    </div>
  </div>

  <div class="forms">
    <form on:submit|preventDefault={handleSubmit}>
      <textarea
        name="reason"
        id=""
        cols="30"
        rows="10"
        bind:value={reason}
        placeholder="Please wrote how did you ended up with the list of the students."
      />
      <button class="next__btn" type="submit">Next</button>
    </form>
  </div>
</div>

<style>
  table,
  th,
  td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 5px 3px;
  }
  table {
    background: var(--lightGray-background);
    width: 100%;
    text-align: center;
    padding: 10px;
  }

  div {
    height: 100%;
    display: flex;
    justify-content: center;
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-content: space-around;
    height: 90%;
  }

  .table {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    width: 80%;
  }

  .table span {
    color: var(--darkGray-text);
    font-size: 12px;
    font-style: italic;
  }

  .forms {
    width: 80%;
    height: 30%;
  }

  table,
  th,
  td {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 5px 3px;
  }
  table {
    background: var(--lightGray-background);
    width: 100%;
    text-align: center;
    padding: 10px;
  }

  .table div {
    width: 100%;
    text-align: left;
  }

  .data-explanation {
    width: 100%;
    text-align: left;
    font-size: 14px;
    color: var(--darkGray-text);
    display: flex;
    flex-direction: column;
    justify-items: end;
  }

  .data-explanation ul {
    width: 95%;
  }

  .data-explanation li {
    padding: 2px 2px;
  }

  .forms form {
    width: 100%;
    height: 80%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .forms textarea {
    background-color: var(--lightGray-background);
    width: 100%;
    height: 80%;
  }
</style>
