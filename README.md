<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Damped Oscillator Calculator</title>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
    <h1>Damped Oscillator Calculator</h1>
    <form id="oscillatorForm">
        <label>Amplitude (A): <input type="number" id="amplitude" value="1" step="0.1"></label><br>
        <label>Damping Coefficient (α): <input type="number" id="damping" value="0.1" step="0.01"></label><br>
        <label>Angular Frequency (ω): <input type="number" id="frequency" value="1" step="0.1"></label><br>
        <label>Phase Angle (φ): <input type="number" id="phase" value="0" step="0.1"></label><br>
        <label>X-Range Start: <input type="number" id="xStart" value="0"></label><br>
        <label>X-Range End: <input type="number" id="xEnd" value="10"></label><br>
        <button type="button" onclick="plotOscillator()">Plot</button>
    </form>
    <div id="plot"></div>

    <script src="oscillator.js"></script>
</body>
</html>


function plotOscillator() {
    // Get values from the form
    const A = parseFloat(document.getElementById("amplitude").value);
    const alpha = parseFloat(document.getElementById("damping").value);
    const omega = parseFloat(document.getElementById("frequency").value);
    const phi = parseFloat(document.getElementById("phase").value);
    const xStart = parseFloat(document.getElementById("xStart").value);
    const xEnd = parseFloat(document.getElementById("xEnd").value);

    // Generate x and y values for plotting
    const xValues = [];
    const yValues = [];
    const step = 0.1; // Adjust for smoothness

    for (let x = xStart; x <= xEnd; x += step) {
        const y = A * Math.exp(-alpha * x) * Math.cos(omega * x + phi);
        xValues.push(x);
        yValues.push(y);
    }

    // Plot using Plotly
    const trace = {
        x: xValues,
        y: yValues,
        type: 'scatter'
    };

    const layout = {
        title: 'Damped Oscillator Plot',
        xaxis: { title: 'x' },
        yaxis: { title: 'y' }
    };

    Plotly.newPlot('plot', [trace], layout);
}
