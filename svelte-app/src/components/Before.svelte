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
      name: "Susan Martinez DVM",
      gre: 304,
      toefl: 91,
      uni: 5,
      sop: 3.5,
      lor: 4.5,
      cgpa: 9.31,
      research: 1,
      chance_of_admit: 0.8508,
    },
    {
      id: 2,
      name: "Steven Horn",
      gre: 310,
      toefl: 96,
      uni: 5,
      sop: 4.5,
      lor: 3.0,
      cgpa: 8.23,
      research: 1,
      chance_of_admit: 0.6039,
    },
    {
      id: 3,
      name: "Michael Stanton",
      gre: 322,
      toefl: 116,
      uni: 5,
      sop: 4.0,
      lor: 3.5,
      cgpa: 9.29,
      research: 1,
      chance_of_admit: 0.8997,
    },
    {
      id: 4,
      name: "Angel Barnett",
      gre: 316,
      toefl: 116,
      uni: 5,
      sop: 5.0,
      lor: 5.0,
      cgpa: 9.77,
      research: 0,
      chance_of_admit: 0.9099,
    },
    {
      id: 5,
      name: "Bobby Fields",
      gre: 285,
      toefl: 93,
      uni: 5,
      sop: 4.0,
      lor: 5.0,
      cgpa: 8.3,
      research: 1,
      chance_of_admit: 0.6175,
    },
    {
      id: 6,
      name: "Kelly Wood",
      gre: 325,
      toefl: 113,
      uni: 5,
      sop: 5.0,
      lor: 4.5,
      cgpa: 8.02,
      research: 1,
      chance_of_admit: 0.6774,
    },
    {
      id: 7,
      name: "Ashlee Davis",
      gre: 285,
      toefl: 118,
      uni: 5,
      sop: 5.0,
      lor: 4.5,
      cgpa: 9.09,
      research: 0,
      chance_of_admit: 0.8195,
    },
    {
      id: 8,
      name: "Justin Martin",
      gre: 336,
      toefl: 96,
      uni: 5,
      sop: 5.0,
      lor: 4.5,
      cgpa: 9.91,
      research: 0,
      chance_of_admit: 0.9397,
    },
    {
      id: 9,
      name: "Destiny Bennett",
      gre: 281,
      toefl: 107,
      uni: 5,
      sop: 4.5,
      lor: 4.0,
      cgpa: 9.53,
      research: 1,
      chance_of_admit: 0.8911,
    },
    {
      id: 10,
      name: "Jeffrey Nguyen",
      gre: 325,
      toefl: 92,
      uni: 5,
      sop: 4.0,
      lor: 3.5,
      cgpa: 8.39,
      research: 0,
      chance_of_admit: 0.6252,
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
