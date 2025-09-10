import React, { useState, useEffect } from "react";

export default function AryamanProfile() {
  const [snake, setSnake] = useState([[5, 5]]);
  const [food, setFood] = useState([10, 10]);
  const [dir, setDir] = useState([0, 1]);

  useEffect(() => {
    const handleKeyDown = (e) => {
      switch (e.key) {
        case "ArrowUp":
          setDir([-1, 0]);
          break;
        case "ArrowDown":
          setDir([1, 0]);
          break;
        case "ArrowLeft":
          setDir([0, -1]);
          break;
        case "ArrowRight":
          setDir([0, 1]);
          break;
        default:
          break;
      }
    };
    window.addEventListener("keydown", handleKeyDown);
    return () => window.removeEventListener("keydown", handleKeyDown);
  }, []);

  useEffect(() => {
    const interval = setInterval(() => {
      setSnake((prev) => {
        const head = prev[0];
        const newHead = [head[0] + dir[0], head[1] + dir[1]];
        const newSnake = [newHead, ...prev];

        if (newHead[0] === food[0] && newHead[1] === food[1]) {
          setFood([
            Math.floor(Math.random() * 15),
            Math.floor(Math.random() * 15),
          ]);
          return newSnake;
        } else {
          newSnake.pop();
          return newSnake;
        }
      });
    }, 200);
    return () => clearInterval(interval);
  }, [dir, food]);

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 via-green-900 to-black flex items-center justify-center p-6">
      <div className="relative w-full max-w-5xl rounded-2xl shadow-2xl overflow-hidden border border-gray-800 bg-black/60 backdrop-blur-md">

        {/* Header */}
        <header className="relative p-8 md:p-12 flex flex-col md:flex-row gap-6 items-center">
          <div className="flex-shrink-0">
            <div className="w-36 h-36 rounded-xl border-2 border-yellow-400 overflow-hidden transform -rotate-3 shadow-lg">
              <img
                src="https://avatars.githubusercontent.com/u/1?v=4"
                alt="Aryaman avatar"
                className="w-full h-full object-cover"
              />
            </div>
          </div>

          <div className="flex-1 text-white">
            <h1 className="text-3xl md:text-4xl font-extrabold tracking-tight leading-tight">
              Sup! I'm <span className="text-emerald-300">Aryaman</span>
            </h1>
            <p className="mt-1 text-lg text-gray-300/90">Gamifying AI — playful, product-minded, & ruthless about UX</p>
          </div>
        </header>

        {/* Stats Section */}
        <section className="p-6 grid md:grid-cols-3 gap-6 border-t border-gray-800 bg-black/40">
          <img src="https://github-readme-stats.vercel.app/api?username=Aryaman-Arya&show_icons=true&theme=dracula&hide_title=true" alt="GitHub stats" className="rounded-lg shadow-md" />
          <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Aryaman-Arya&layout=compact&theme=dracula&hide_title=true" alt="Top Languages" className="rounded-lg shadow-md" />
          <img src="https://github-readme-streak-stats.herokuapp.com/?user=Aryaman-Arya&theme=dracula&hide_border=true" alt="Streak Stats" className="rounded-lg shadow-md" />
        </section>

        {/* Skills */}
        <section className="p-6 border-t border-gray-800">
          <h2 className="text-xl font-bold text-white mb-4">Skills that pay the bills:</h2>
          <div className="flex flex-wrap gap-3">
            <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white" alt="Python" />
            <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white" alt="TensorFlow" />
            <img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white" alt="Docker" />
            <img src="https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white" alt="Git" />
          </div>
        </section>

        {/* Snake Game */}
        <section className="p-8 border-t border-gray-800 bg-black/40">
          <h2 className="text-xl font-bold text-white mb-4">Snake Mode: Hack the Matrix</h2>
          <div className="grid grid-cols-15 gap-0.5 bg-gray-800 w-max mx-auto p-1 rounded-md">
            {Array.from({ length: 15 }).map((_, row) =>
              Array.from({ length: 15 }).map((_, col) => {
                const isSnake = snake.some(([r, c]) => r === row && c === col);
                const isFood = food[0] === row && food[1] === col;
                return (
                  <div
                    key={`${row}-${col}`}
                    className={`w-4 h-4 ${
                      isSnake
                        ? "bg-emerald-400"
                        : isFood
                        ? "bg-red-500"
                        : "bg-gray-900"
                    } rounded-sm`}
                  ></div>
                );
              })
            )}
          </div>
        </section>

        {/* Contact */}
        <section className="p-6 border-t border-gray-800 text-white">
          <h2 className="text-xl font-bold mb-2">Hit me up if you wanna collab, chat AI, or just vibe:</h2>
          <a
            href="https://www.linkedin.com/in/aryaman-arya"
            className="inline-block mt-2 px-4 py-2 bg-emerald-600 hover:bg-emerald-700 rounded-md text-white text-sm font-semibold shadow-md transition"
          >
            Connect on LinkedIn
          </a>
        </section>

        {/* Footer */}
        <footer className="border-t border-gray-800 p-4 flex items-center justify-between">
          <div className="text-xs text-gray-400">Built with focus, caffeine, and stubbornness.</div>
          <div className="text-xs text-gray-400 font-mono tracking-wider">Portfolio · Resume · Projects</div>
        </footer>
      </div>
    </div>
  );
}
