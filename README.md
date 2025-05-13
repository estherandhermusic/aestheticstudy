# aestheticstudy
# aestheticstudy
import React, { useState, useEffect } from "react";
import MotivationalQuotes from "../Motivation/MotivationalQuotes";

const Timer = () => {
  const [time, setTime] = useState(0);
  const [isRunning, setIsRunning] = useState(false);

  useEffect(() => {
    let timer;
    if (isRunning) {
      timer = setInterval(() => {
        setTime((prevTime) => prevTime + 1);
      }, 1000);
    } else {
      clearInterval(timer);
    }
    return () => clearInterval(timer);
  }, [isRunning]);

  useEffect(() => {
    if (time > 0 && time % 600 === 0) {
      // 10 minutos = 600 segundos
      alert("¡Frase motivadora: 'El esfuerzo siempre da frutos!'");
    }
  }, [time]);

  const handleStartStop = () => {
    setIsRunning(!isRunning);
  };

  const handleReset = () => {
    setIsRunning(false);
    setTime(0);
  };

  return (
    <div className="timer">
      <h1>Temporizador</h1>
      <h2>{new Date(time * 1000).toISOString().substr(11, 8)}</h2>
      <button onClick={handleStartStop}>
        {isRunning ? "Pausar" : "Iniciar"}
      </button>
      <button onClick={handleReset}>Reiniciar</button>
      <MotivationalQuotes />
    </div>
  );
};

export default Timer;
