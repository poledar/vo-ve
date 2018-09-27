const canvas = document.querySelector('#canvas');
const context = canvas.getContext('2d');
const source = new Image();
const input = document.querySelector('#texto');
const offy = document.querySelector('#offy');
const offx = document.querySelector('#offx');
const boxs = document.querySelector('#boxs');
const download = document.querySelector('#download');

function wrapText(x, y, text, fontsize, fontface, maxwidth) {
    const startingY = y;
    const words = text.split(' ');
    const lineHeight = fontsize * 1.286;
    let line = '';
    let space = '';
    context.font = fontsize + "px " + fontface;
    context.textAlign = 'left';
    context.textBaseline = 'top'
    for (var n = 0; n < words.length; n++) {
        const testLine = line + space + words[n];
        space = ' ';
        if (context.measureText(testLine).width > maxwidth) {
            context.fillText(line, x, y);
            line = words[n] + ' ';
            y += lineHeight;
            space = '';
        } else {
            line = testLine;
        }
    }
    context.fillText(line, x, y);
    return (y + lineHeight - startingY);
}

function draw() {
    context.drawImage(source, 0, 0);
    const height = source.height * (offy.value / 100);
    const width = source.width * (offx.value / 100);
    const size = source.width * (boxs.value / 100);
    wrapText(width, height, input.value, 24, 'sans-serif', size);
    const data = canvas.toDataURL("image/png").replace("image/png", "image/octet-stream");
    download.setAttribute("href", data);
}

source.addEventListener('load', () => {
    canvas.height = source.height;
    canvas.width = source.width;
    context.fillStyle = 'white';
    draw();
    input.addEventListener('input', () => draw());
    offx.addEventListener('input', () => draw());
    offy.addEventListener('input', () => draw());
    boxs.addEventListener('input', () => draw());
});
source.src = 'caveira.jpg';
