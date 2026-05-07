# Animasi Transformasi Titik

Program berikut menampilkan animasi transformasi titik mendekati sumbu X.

```{code-cell} python
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import rc

rc('animation', html='jshtml')

points = {
    "A": (2, 3),
    "B": (2, 4),
    "C": (3, 4),
    "D": (3, 3)
}

garis = [
    ("A", "B"),
    ("B", "C"),
    ("C", "D"),
    ("D", "A")
]

fig, ax = plt.subplots(figsize=(6,6))

def update(frame):

    ax.clear()

    scale_y = 1 - frame / 100

    posisi_baru = {}

    for nama, (x, y) in points.items():

        y_baru = y * scale_y

        posisi_baru[nama] = (x, y_baru)

        ax.scatter(x, y_baru)

        ax.text(x + 0.05, y_baru + 0.05, nama)

    for p1, p2 in garis:

        x1, y1 = posisi_baru[p1]
        x2, y2 = posisi_baru[p2]

        ax.plot([x1, x2], [y1, y2])

    ax.set_xlim(0,5)
    ax.set_ylim(-5,5)

    ax.axhline(0)
    ax.axvline(0)

    ax.grid(True)

ani = animation.FuncAnimation(
    fig,
    update,
    frames=101,
    interval=50
)

ani
```