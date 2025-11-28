index.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Gen-4 Season 4 Standings</title>

<style>
    body {
        background-color: #081421;
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 40px;
        color: #000;
    }

    .container {
        max-width: 1100px;
        margin: auto;
        background: #0b1d36;
        padding: 20px;
        border-radius: 10px;
    }

    h1 {
        text-align: center;
        color: white;
        margin-bottom: 25px;
        font-size: 32px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        border-radius: 8px;
        overflow: hidden;
    }

    th {
        background-color: #102544;
        color: #000;   /* HEADER TEXT BLACK */
        padding: 12px;
        font-size: 15px;
    }

    td {
        padding: 14px;
        color: #000;   /* ROW TEXT BLACK */
        font-size: 15px;
        background-color: #0b1d36;
    }

    tbody tr:nth-child(even) td {
        background-color: #142e4f;   /* lighter navy */
    }

    tbody tr:hover td {
        background-color: #1f3c63;
        transition: 0.2s;
    }

    .driver-cell {
        display: flex;
        align-items: center;
        gap: 10px;
        color: #000;
    }

    .driver-photo {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        object-fit: cover;
        border: 2px solid #000;
    }
</style>
</head>

<body>

<div class="container">
    <h1>Gen-4 Season 4 Final Standings</h1>

    <table>
        <thead>
            <tr>
                <th>Pos.</th>
                <th>Driver</th>
                <th>Pts</th>
                <th>Pts-</th>
                <th>Wins</th>
                <th>Top 5s</th>
                <th>Top 10s</th>
                <th>Starts</th>
                <th>DNF’s</th>
            </tr>
        </thead>

        <tbody>

            <!-- 1 -->
            <tr>
                <td>1</td>
                <td class="driver-cell">
                    Terry Labonte
                </td>
                <td>501</td><td>-</td><td>1</td><td>10</td><td>14</td><td>20</td><td>0</td>
            </tr>

            <!-- 2 -->
            <tr>
                <td>2</td>
                <td class="driver-cell">Jeff Gordon</td>
                <td>500</td><td>-1</td><td>4</td><td>10</td><td>13</td><td>20</td><td>2</td>
            </tr>

            <!-- 3 -->
            <tr>
                <td>3</td>
                <td class="driver-cell">Dale Jarrett</td>
                <td>456</td><td>-45</td><td>2</td><td>5</td><td>12</td><td>20</td><td>3</td>
            </tr>

            <!-- 4 -->
            <tr><td>4</td><td class="driver-cell">Dale Earnhardt</td><td>454</td><td>-47</td><td>2</td><td>7</td><td>9</td><td>20</td><td>1</td></tr>
            
            <!-- 5 -->
            <tr><td>5</td><td class="driver-cell">Jeff Burton</td><td>448</td><td>-53</td><td>2</td><td>7</td><td>9</td><td>20</td><td>2</td></tr>

            <!-- 6 -->
            <tr><td>6</td><td class="driver-cell">Bobby Labonte</td><td>445</td><td>-56</td><td>1</td><td>6</td><td>11</td><td>20</td><td>1</td></tr>

            <!-- 7 -->
            <tr><td>7</td><td class="driver-cell">Dale Earnhardt Jr.</td><td>431</td><td>-70</td><td>1</td><td>7</td><td>11</td><td>20</td><td>1</td></tr>

            <!-- 8 -->
            <tr><td>8</td><td class="driver-cell">Bill Elliott</td><td>417</td><td>-84</td><td>0</td><td>7</td><td>9</td><td>20</td><td>2</td></tr>

            <!-- continue with rest of drivers... -->
        </tbody>
    </table>
</div>

</body>
</html>
