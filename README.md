# 12 Coins Problem – Recursive AI Solution (Animated in Python)

```python
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from time import sleep

# Hidden truth (for demonstration)
FAKE_COIN = 4
FAKE_TYPE = "light"  # "heavy" or "light"

def weight(coin):
    if coin != FAKE_COIN:
        return 1
    return 2 if FAKE_TYPE == "heavy" else 0

# Recursive AI reasoning steps (predefined classic solution path)
steps = [
    ("Weighing 1", [1,2,3,4], [5,6,7,8]),
    ("Weighing 2", [1,2,5], [3,9,10]),
    ("Weighing 3", [4], [6])
]

fig, ax = plt.subplots()
ax.set_xlim(-1, 1)
ax.set_ylim(-1, 1)
ax.axis("off")

beam, = ax.plot([-0.6, 0.6], [0, 0], linewidth=4)
text = ax.text(0, -0.6, "", ha="center", fontsize=12)

def animate(i):
    label, left, right = steps[i]
    lw = sum(weight(c) for c in left)
    rw = sum(weight(c) for c in right)

    if lw > rw:
        beam.set_ydata([0.1, -0.1])
        outcome = "Left Heavier"
    elif rw > lw:
        beam.set_ydata([-0.1, 0.1])
        outcome = "Right Heavier"
    else:
        beam.set_ydata([0, 0])
        outcome = "Balanced"

    text.set_text(
        f"{label}\nLeft: {left}  Right: {right}\nOutcome: {outcome}"
    )
    return beam, text

ani = animation.FuncAnimation(
    fig,
    animate,
    frames=len(steps),
    interval=2000,
    repeat=False
)

plt.show()
