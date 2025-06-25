// Rubik's Cube Simulator Logic in JavaScript with full cube net view

class RubiksCube {
  constructor() {
    this.reset();
  }

  reset() {
    this.faces = {
      U: Array(9).fill('w'),
      D: Array(9).fill('y'),
      F: Array(9).fill('g'),
      B: Array(9).fill('b'),
      L: Array(9).fill('o'),
      R: Array(9).fill('r')
    };
    this.scrambleMoves = [];
  }

  getStateString() {
    return [
      'U: ' + this.faces.U.join(''),
      'L: ' + this.faces.L.join(''),
      'F: ' + this.faces.F.join(''),
      'R: ' + this.faces.R.join(''),
      'B: ' + this.faces.B.join(''),
      'D: ' + this.faces.D.join('')
    ].join('\n');
  }

  rotateFaceClockwise(face) {
    const f = face.slice();
    return [
      f[6], f[3], f[0],
      f[7], f[4], f[1],
      f[8], f[5], f[2]
    ];
  }

  rotate(face) {
    this.scrambleMoves.push(face);
    const F = this.faces;

    if (face === 'F') {
      F.F = this.rotateFaceClockwise(F.F);

      const tempTop = [F.U[6], F.U[7], F.U[8]];
      const tempRight = [F.R[0], F.R[3], F.R[6]];
      const tempBottom = [F.D[2], F.D[1], F.D[0]];
      const tempLeft = [F.L[8], F.L[5], F.L[2]];

      [F.U[6], F.U[7], F.U[8]] = tempLeft;
      [F.R[0], F.R[3], F.R[6]] = tempTop;
      [F.D[2], F.D[1], F.D[0]] = tempRight;
      [F.L[8], F.L[5], F.L[2]] = tempBottom;
    }
  }

  scramble() {
    const moves = ['F'];
    this.scrambleMoves = [];
    for (let i = 0; i < 10; i++) {
      const move = moves[Math.floor(Math.random() * moves.length)];
      this.rotate(move);
    }
  }

  solve() {
    return this.scrambleMoves.slice().reverse().map(m => m + "'");
  }
}

const cube = new RubiksCube();

function updateDisplay() {
  const cubeDisplay = document.getElementById("cube-display");
  cubeDisplay.innerHTML = '';

  const F = cube.faces;
  const colorMap = {
    w: 'bg-white',
    y: 'bg-yellow-300',
    g: 'bg-green-500',
    b: 'bg-blue-500',
    o: 'bg-orange-500',
    r: 'bg-red-500'
  };

  const createFace = (faceArray) => {
    return faceArray.map(color => {
      const div = document.createElement('div');
      div.className = `w-8 h-8 ${colorMap[color]} border border-black`;
      return div;
    });
  };

  const faceGrid = document.createElement('div');
  faceGrid.className = 'grid grid-cols-12 gap-1 justify-center items-center';

  // First row: U (centered)
  for (let i = 0; i < 12; i++) {
    if (i < 3 || i > 5) {
      faceGrid.appendChild(document.createElement('div'));
    } else {
      faceGrid.appendChild(...createFace(F.U).slice(i - 3, i - 2));
    }
  }

  // Middle rows: L F R B
  for (let row = 0; row < 3; row++) {
    const faces = ['L', 'F', 'R', 'B'];
    for (let face of faces) {
      const rowSlice = F[face].slice(row * 3, row * 3 + 3);
      for (let color of rowSlice) {
        const div = document.createElement('div');
        div.className = `w-8 h-8 ${colorMap[color]} border border-black`;
        faceGrid.appendChild(div);
      }
    }
  }

  // Last row: D (centered)
  for (let i = 0; i < 12; i++) {
    if (i < 3 || i > 5) {
      faceGrid.appendChild(document.createElement('div'));
    } else {
      faceGrid.appendChild(...createFace(F.D).slice(i - 3, i - 2));
    }
  }

  cubeDisplay.appendChild(faceGrid);
  document.getElementById("steps").innerHTML = `<pre>${cube.getStateString()}</pre>`;
}

function rotateFront() {
  cube.rotate('F');
  updateDisplay();
}

function scrambleCube() {
  cube.scramble();
  updateDisplay();
}

function solveCube() {
  const steps = cube.solve();
  const stepContainer = document.getElementById("steps");
  stepContainer.innerHTML = `<h2 class="text-xl font-semibold mb-2">Solving Steps:</h2>`;
  let i = 0;

  const interval = setInterval(() => {
    if (i >= steps.length) {
      clearInterval(interval);
      return;
    }
    const move = steps[i];
    const div = document.createElement("div");
    div.textContent = `Step ${i + 1}: ${move}`;
    stepContainer.appendChild(div);
    i++;
  }, 400);
}

function resetCube() {
  cube.reset();
  updateDisplay();
}

updateDisplay();
