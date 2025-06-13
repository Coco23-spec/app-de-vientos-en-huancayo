import React, { useState, useEffect, useCallback, useMemo } from 'react';
import { Wind, MapPin, AlertTriangle, Activity, Settings, Home, Map, Bell, Thermometer, Droplets } from 'lucide-react';

const VientoSeguroApp = () => {
  const [currentWind, setCurrentWind] = useState({
    speed: 0,
    direction: 0,
    cardinal: 'E',
    force: 0,
    components: { fx: 0, fy: 0 },
    temperature: 18,
    humidity: 65,
    pressure: 710
  });
  
  const [alerts, setAlerts] = useState([]);
  const [activeTab, setActiveTab] = useState('monitor');
  const [simulationActive, setSimulationActive] = useState(false);
  const [dataIndex, setDataIndex] = useState(0);
  const [windHistory, setWindHistory] = useState([]);

  // Datos de simulación mejorados con más variables
  const windData = useMemo(() => [
    { speed: 25, direction: 90, cardinal: 'E', time: '08:00', temp: 18, humidity: 65, pressure: 710 },
    { speed: 32, direction: 135, cardinal: 'SE', time: '08:05', temp: 19, humidity: 62, pressure: 708 },
    { speed: 28, direction: 90, cardinal: 'E', time: '08:10', temp: 20, humidity: 60, pressure: 712 },
    { speed: 41, direction: 135, cardinal: 'SE', time: '08:15', temp: 21, humidity: 58, pressure: 705 },
    { speed: 35, direction: 45, cardinal: 'NE', time: '08:20', temp: 22, humidity: 55, pressure: 708 },
    { speed: 15, direction: 0, cardinal: 'N', time: '08:25', temp: 20, humidity: 62, pressure: 714 },
    { speed: 48, direction: 180, cardinal: 'S', time: '08:30', temp: 23, humidity: 52, pressure: 702 },
    { speed: 22, direction: 270, cardinal: 'O', time: '08:35', temp: 21, humidity: 58, pressure: 709 }
  ], []);

  // Función mejorada para calcular fuerza y componentes
  const calculateWindForce = useCallback((speed, direction, pressure = 710) => {
    const speedMs = speed / 3.6; // km/h a m/s
    // Ajustar densidad del aire según presión atmosférica
    const rho = 0.91 * (pressure / 710); // densidad ajustada por presión
    const area = 2; // m²
    const cd = 1.3; // coeficiente de arrastre
    
    const force = 0.5 * rho * speedMs * speedMs * area * cd;
    const radians = (direction * Math.PI) / 180;
    
    return {
      total: Math.round(force * 10) / 10, // Más precisión
      fx: Math.round(force * Math.cos(radians) * 10) / 10,
      fy: Math.round(force * Math.sin(radians) * 10) / 10
    };
  }, []);

  // Función mejorada para determinar nivel de alerta
  const getAlertLevel = useCallback((speed, temperature, pressure) => {
    // Factores de riesgo adicionales
    const tempFactor = temperature > 25 ? 1.1 : 1;
    const pressureFactor = pressure < 705 ? 1.15 : 1;
    const adjustedSpeed = speed * tempFactor * pressureFactor;

    if (adjustedSpeed >= 45) return { 
      level: 'rojo', 
      text: 'PELIGRO EXTREMO', 
      color: 'bg-red-600',
      bgColor: 'bg-red-50',
      textColor: 'text-red-700',
      borderColor: 'border-red-500'
    };
    if (adjustedSpeed >= 35) return { 
      level: 'naranja', 
      text: 'ALERTA ALTA', 
      color: 'bg-orange-500',
      bgColor: 'bg-orange-50',
      textColor: 'text-orange-700',
      borderColor: 'border-orange-500'
    };
    if (adjustedSpeed >= 25) return { 
      level: 'amarillo', 
      text: 'PRECAUCIÓN', 
      color: 'bg-yellow-500',
      bgColor: 'bg-yellow-50',
      textColor: 'text-yellow-700',
      borderColor: 'border-yellow-500'
    };
    return { 
      level: 'verde', 
      text: 'CONDICIONES NORMALES', 
      color: 'bg-green-500',
      bgColor: 'bg-green-50',
      textColor: 'text-green-700',
      borderColor: 'border-green-500'
    };
  }, []);

  // Simulación mejorada con historial
  useEffect(() => {
    if (simulationActive) {
      const interval = setInterval(() => {
        const data = windData[dataIndex % windData.length];
        const force = calculateWindForce(data.speed, data.direction, data.pressure);
        const alert = getAlertLevel(data.speed, data.temp, data.pressure);
        
        const newWindData = {
          speed: data.speed,
          direction: data.direction,
          cardinal: data.cardinal,
          force: force.total,
          components: { fx: force.fx, fy: force.fy },
          temperature: data.temp,
          humidity: data.humidity,
          pressure: data.pressure,
          timestamp: new Date().toLocaleTimeString()
        };

        setCurrentWind(newWindData);

        // Actualizar historial (últimas 20 mediciones)
        setWindHistory(prev => [newWindData, ...prev.slice(0, 19)]);

        // Generar alerta solo si hay cambio significativo de nivel
        if (alert.level !== 'verde') {
          const newAlert = {
            id: Date.now(),
            level: alert.level,
            text: alert.text,
            speed: data.speed,
            direction: data.cardinal,
            temperature: data.temp,
            pressure: data.pressure,
            time: new Date().toLocaleTimeString(),
            message: `${alert.text}: Viento de ${data.speed} km/h desde el ${data.cardinal}. Temp: ${data.temp}°C, Presión: ${data.pressure} hPa`
          };
          setAlerts(prev => {
            // Evitar alertas duplicadas consecutivas
            if (prev.length > 0 && prev[0].level === alert.level && prev[0].speed === data.speed) {
              return prev;
            }
            return [newAlert, ...prev.slice(0, 9)]; // Máximo 10 alertas
          });
        }

        setDataIndex(prev => prev + 1);
      }, 2500); // Intervalo ligeramente más rápido

      return () => clearInterval(interval);
    }
  }, [simulationActive, dataIndex, windData, calculateWindForce, getAlertLevel]);

  // Estadísticas del historial
  const windStats = useMemo(() => {
    if (windHistory.length === 0) return null;
    
    const speeds = windHistory.map(w => w.speed);
    const maxSpeed = Math.max(...speeds);
    const avgSpeed = Math.round(speeds.reduce((a, b) => a + b, 0) / speeds.length);
    const minSpeed = Math.min(...speeds);
    
    return { max: maxSpeed, avg: avgSpeed, min: minSpeed };
  }, [windHistory]);

  // Componente Monitor Principal mejorado
  const MonitorTab = () => {
    const alert = getAlertLevel(currentWind.speed, currentWind.temperature, currentWind.pressure);
    
    return (
      <div className="p-4 space-y-6">
        {/* Header con ubicación */}
        <div className="flex items-center justify-between">
          <div className="flex items-center space-x-2">
            <MapPin className="text-blue-600" size={20} />
            <span className="font-semibold text-gray-800">Huancayo, Junín</span>
          </div>
          <div className="text-sm text-gray-600">3,249 msnm</div>
        </div>

        {/* Control de simulación mejorado */}
        <div className={`${simulationActive ? 'bg-green-50 border-green-200' : 'bg-blue-50 border-blue-200'} p-4 rounded-lg border`}>
          <div className="flex items-center justify-between mb-2">
            <span className="text-sm font-medium text-gray-700">
              {simulationActive ? 'Monitoreo Activo' : 'Sistema Inactivo'}
            </span>
            {simulationActive && (
              <div className="flex items-center text-green-600">
                <Activity className="animate-pulse mr-1" size={16} />
                <span className="text-xs">En vivo</span>
              </div>
            )}
          </div>
          <button
            onClick={() => setSimulationActive(!simulationActive)}
            className={`w-full py-2 px-4 rounded-lg font-semibold transition-colors ${
              simulationActive 
                ? 'bg-red-500 hover:bg-red-600 text-white' 
                : 'bg-blue-600 hover:bg-blue-700 text-white'
            }`}
          >
            {simulationActive ? '⏹️ Detener Monitoreo' : '▶️ Iniciar Monitoreo'}
          </button>
        </div>

        {/* Medición actual mejorada */}
        <div className="bg-white rounded-xl shadow-lg p-6">
          <div className="text-center mb-4">
            <div className="flex items-center justify-center mb-2">
              <Wind className="text-blue-600 mr-2" size={24} />
              <span className="text-lg font-semibold">Condiciones Actuales</span>
            </div>
            <div className="text-4xl font-bold text-blue-800 mb-1">
              {currentWind.speed} <span className="text-lg">km/h</span>
            </div>
            <div className="text-gray-600">
              {currentWind.cardinal} ({currentWind.direction}°)
            </div>
            {currentWind.timestamp && (
              <div className="text-xs text-gray-500 mt-1">
                Última actualización: {currentWind.timestamp}
              </div>
            )}
          </div>

          {/* Nivel de alerta mejorado */}
          <div className="mb-4">
            <div className={`${alert.color} text-white text-center py-3 px-4 rounded-lg font-semibold shadow-md`}>
              {alert.text}
            </div>
          </div>

          {/* Variables ambientales */}
          <div className="grid grid-cols-3 gap-3 mb-4">
            <div className="text-center p-3 bg-blue-50 rounded-lg">
              <Thermometer className="mx-auto mb-1 text-blue-600" size={20} />
              <div className="font-semibold text-blue-800">{currentWind.temperature}°C</div>
              <div className="text-xs text-gray-600">Temperatura</div>
            </div>
            <div className="text-center p-3 bg-cyan-50 rounded-lg">
              <Droplets className="mx-auto mb-1 text-cyan-600" size={20} />
              <div className="font-semibold text-cyan-800">{currentWind.humidity}%</div>
              <div className="text-xs text-gray-600">Humedad</div>
            </div>
            <div className="text-center p-3 bg-purple-50 rounded-lg">
              <Activity className="mx-auto mb-1 text-purple-600" size={20} />
              <div className="font-semibold text-purple-800">{currentWind.pressure}</div>
              <div className="text-xs text-gray-600">hPa</div>
            </div>
          </div>

          {/* Análisis vectorial */}
          <div className="bg-gray-50 p-4 rounded-lg">
            <h4 className="font-semibold mb-3 text-gray-800">Análisis de Fuerzas</h4>
            <div className="grid grid-cols-3 gap-4 text-sm">
              <div className="text-center">
                <div className="font-bold text-blue-600 text-lg">{currentWind.force}N</div>
                <div className="text-gray-600">Fuerza Total</div>
              </div>
              <div className="text-center">
                <div className="font-bold text-green-600 text-lg">{currentWind.components.fx}N</div>
                <div className="text-gray-600">Componente X</div>
              </div>
              <div className="text-center">
                <div className="font-bold text-purple-600 text-lg">{currentWind.components.fy}N</div>
                <div className="text-gray-600">Componente Y</div>
              </div>
            </div>
          </div>
        </div>

        {/* Estadísticas del historial */}
        {windStats && (
          <div className="bg-white rounded-xl shadow-lg p-4">
            <h4 className="font-semibold mb-3 text-gray-800">Estadísticas Recientes</h4>
            <div className="grid grid-cols-3 gap-4 text-sm">
              <div className="text-center">
                <div className="font-bold text-red-600">{windStats.max} km/h</div>
                <div className="text-gray-600">Máximo</div>
              </div>
              <div className="text-center">
                <div className="font-bold text-blue-600">{windStats.avg} km/h</div>
                <div className="text-gray-600">Promedio</div>
              </div>
              <div className="text-center">
                <div className="font-bold text-green-600">{windStats.min} km/h</div>
                <div className="text-gray-600">Mínimo</div>
              </div>
            </div>
          </div>
        )}

        {/* Rosa de vientos mejorada */}
        <div className="bg-white rounded-xl shadow-lg p-6">
          <h4 className="font-semibold mb-4 text-center">Rosa de Vientos</h4>
          <div className="relative w-48 h-48 mx-auto">
            <svg viewBox="0 0 200 200" className="w-full h-full">
              {/* Círculos de referencia */}
              <circle cx="100" cy="100" r="80" fill="none" stroke="#e5e7eb" strokeWidth="1" />
              <circle cx="100" cy="100" r="60" fill="none" stroke="#e5e7eb" strokeWidth="1" />
              <circle cx="100" cy="100" r="40" fill="none" stroke="#e5e7eb" strokeWidth="1" />
              <circle cx="100" cy="100" r="20" fill="none" stroke="#e5e7eb" strokeWidth="1" />
              
              {/* Líneas cardinales */}
              <line x1="100" y1="20" x2="100" y2="180" stroke="#d1d5db" strokeWidth="1" />
              <line x1="20" y1="100" x2="180" y2="100" stroke="#d1d5db" strokeWidth="1" />
              <line x1="38" y1="38" x2="162" y2="162" stroke="#d1d5db" strokeWidth="0.5" />
              <line x1="162" y1="38" x2="38" y2="162" stroke="#d1d5db" strokeWidth="0.5" />
              
              {/* Labels cardinales */}
              <text x="100" y="15" textAnchor="middle" className="fill-gray-600 text-xs font-bold">N</text>
              <text x="185" y="105" textAnchor="middle" className="fill-gray-600 text-xs font-bold">E</text>
              <text x="100" y="195" textAnchor="middle" className="fill-gray-600 text-xs font-bold">S</text>
              <text x="15" y="105" textAnchor="middle" className="fill-gray-600 text-xs font-bold">O</text>
              
              {/* Flecha direccional del viento mejorada */}
              {(() => {
                const angle = currentWind.direction;
                const intensity = Math.min(currentWind.speed / 50, 1);
                const radius = 70 * intensity;
                const x = 100 + radius * Math.cos((angle - 90) * Math.PI / 180);
                const y = 100 + radius * Math.sin((angle - 90) * Math.PI / 180);
                
                // Color según intensidad
                const color = intensity > 0.8 ? '#dc2626' : intensity > 0.6 ? '#ea580c' : intensity > 0.4 ? '#d97706' : '#3b82f6';
                
                return (
                  <g>
                    <line x1="100" y1="100" x2={x} y2={y} stroke={color} strokeWidth="4" strokeLinecap="round" />
                    <circle cx={x} cy={y} r="6" fill={color} />
                    <circle cx="100" cy="100" r="3" fill="#374151" />
                  </g>
                );
              })()}
            </svg>
          </div>
          <div className="text-center mt-2 text-sm text-gray-600">
            Intensidad: {Math.round((currentWind.speed / 50) * 100)}%
          </div>
        </div>
      </div>
    );
  };

  // Componente Mapa de Riesgo mejorado
  const MapTab = () => (
    <div className="p-4 space-y-4">
      <h3 className="text-lg font-semibold text-gray-800 flex items-center">
        <Map className="mr-2" size={20} />
        Mapa de Riesgo - Valle del Mantaro
      </h3>
      
      <div className="bg-white rounded-xl shadow-lg p-4">
        <div className="bg-gradient-to-br from-green-100 via-blue-100 to-purple-100 h-80 rounded-lg relative overflow-hidden">
          {/* Simulación mejorada de mapa */}
          <div className="absolute inset-0 flex items-center justify-center">
            <div className="text-center">
              <div className="text-3xl mb-2">🏔️</div>
              <div className="text-gray-700 font-bold text-lg">Valle del Mantaro</div>
              <div className="text-gray-600">Huancayo Centro</div>
              <div className="text-xs text-gray-500 mt-1">3,249 msnm</div>
            </div>
          </div>
          
          {/* Zonas de riesgo con animación */}
          <div className="absolute top-6 left-6 bg-red-500 w-10 h-10 rounded-full opacity-80 animate-pulse shadow-lg flex items-center justify-center">
            <span className="text-white text-xs font-bold">!</span>
          </div>
          <div className="absolute top-16 right-12 bg-orange-500 w-8 h-8 rounded-full opacity-75 shadow-md"></div>
          <div className="absolute bottom-12 left-16 bg-yellow-500 w-9 h-9 rounded-full opacity-75 shadow-md"></div>
          <div className="absolute bottom-6 right-6 bg-green-500 w-6 h-6 rounded-full opacity-75 shadow-sm"></div>
          <div className="absolute top-1/2 left-1/3 bg-blue-500 w-4 h-4 rounded-full opacity-60"></div>
          
          {/* Efectos de viento */}
          <div className="absolute top-0 left-0 w-full h-full">
            {[...Array(8)].map((_, i) => (
              <div 
                key={i}
                className="absolute w-1 h-6 bg-white opacity-20 animate-pulse"
                style={{
                  left: `${20 + i * 10}%`,
                  top: `${30 + (i % 3) * 20}%`,
                  transform: `rotate(${currentWind.direction}deg)`,
                  animationDelay: `${i * 0.2}s`
                }}
              />
            ))}
          </div>
        </div>
        
        {/* Leyenda mejorada */}
        <div className="mt-4 space-y-2">
          <h5 className="font-semibold text-sm text-gray-700">Niveles de Riesgo</h5>
          <div className="grid grid-cols-1 gap-2 text-xs">
            <div className="flex items-center justify-between p-2 bg-red-50 rounded border-l-4 border-red-500">
              <div className="flex items-center">
                <div className="w-3 h-3 bg-red-500 rounded-full mr-2"></div>
                <span className="font-medium">Peligro Extremo</span>
              </div>
              <span className="text-red-600 font-bold">&gt;45 km/h</span>
            </div>
            <div className="flex items-center justify-between p-2 bg-orange-50 rounded border-l-4 border-orange-500">
              <div className="flex items-center">
                <div className="w-3 h-3 bg-orange-500 rounded-full mr-2"></div>
                <span className="font-medium">Alerta Alta</span>
              </div>
              <span className="text-orange-600 font-bold">35-45 km/h</span>
            </div>
            <div className="flex items-center justify-between p-2 bg-yellow-50 rounded border-l-4 border-yellow-500">
              <div className="flex items-center">
                <div className="w-3 h-3 bg-yellow-500 rounded-full mr-2"></div>
                <span className="font-medium">Precaución</span>
              </div>
              <span className="text-yellow-600 font-bold">25-35 km/h</span>
            </div>
            <div className="flex items-center justify-between p-2 bg-green-50 rounded border-l-4 border-green-500">
              <div className="flex items-center">
                <div className="w-3 h-3 bg-green-500 rounded-full mr-2"></div>
                <span className="font-medium">Condiciones Normales</span>
              </div>
              <span className="text-green-600 font-bold">&lt;25 km/h</span>
            </div>
          </div>
        </div>
      </div>

      {/* Sectores críticos mejorados */}
      <div className="bg-white rounded-xl shadow-lg p-4">
        <h4 className="font-semibold mb-3 flex items-center">
          <AlertTriangle className="mr-2 text-orange-500" size={18} />
          Sectores de Mayor Riesgo
        </h4>
        <div className="space-y-3">
          <div className="flex justify-between items-center p-3 bg-red-50 rounded-lg border-l-4 border-red-500">
            <div>
              <div className="font-medium text-sm">El Tambo - Zona de Antenas</div>
              <div className="text-xs text-gray-600">Exposición elevada, terreno abierto</div>
            </div>
            <span className="text-xs text-red-700 font-bold bg-red-200 px-2 py-1 rounded">CRÍTICO</span>
          </div>
          <div className="flex justify-between items-center p-3 bg-orange-50 rounded-lg border-l-4 border-orange-500">
            <div>
              <div className="font-medium text-sm">Chilca - Sector Techos</div>
              <div className="text-xs text-gray-600">Estructuras vulnerables</div>
            </div>
            <span className="text-xs text-orange-700 font-bold bg-orange-200 px-2 py-1 rounded">ALTO</span>
          </div>
          <div className="flex justify-between items-center p-3 bg-yellow-50 rounded-lg border-l-4 border-yellow-500">
            <div>
              <div className="font-medium text-sm">Huancayo Centro</div>
              <div className="text-xs text-gray-600">Zona urbana protegida</div>
            </div>
            <span className="text-xs text-yellow-700 font-bold bg-yellow-200 px-2 py-1 rounded">MEDIO</span>
          </div>
          <div className="flex justify-between items-center p-3 bg-green-50 rounded-lg border-l-4 border-green-500">
            <div>
              <div className="font-medium text-sm">San Carlos - Residencial</div>
              <div className="text-xs text-gray-600">Área de bajo riesgo</div>
            </div>
            <span className="text-xs text-green-700 font-bold bg-green-200 px-2 py-1 rounded">BAJO</span>
          </div>
        </div>
      </div>

      {/* Recomendaciones de seguridad */}
      <div className="bg-white rounded-xl shadow-lg p-4">
        <h4 className="font-semibold mb-3 text-gray-800">Recomendaciones de Seguridad</h4>
        <div className="space-y-2 text-sm">
          <div className="flex items-start space-x-2">
            <span className="text-blue-600 font-bold">•</span>
            <span>Evitar actividades al aire libre en zonas rojas</span>
          </div>
          <div className="flex items-start space-x-2">
            <span className="text-blue-600 font-bold">•</span>
            <span>Asegurar objetos sueltos en patios y terrazas</span>
          </div>
          <div className="flex items-start space-x-2">
            <span className="text-blue-600 font-bold">•</span>
            <span>Revisar estado de techos y estructuras</span>
          </div>
          <div className="flex items-start space-x-2">
            <span className="text-blue-600 font-bold">•</span>
            <span>Mantenerse informado de las condiciones meteorológicas</span>
          </div>
        </div>
      </div>
    </div>
  );

  // Componente Alertas mejorado
  const AlertsTab = () => (
    <div className="p-4 space-y-4">
      <div className="flex items-center justify-between">
        <h3 className="text-lg font-semibold text-gray-800 flex items-center">
          <Bell className="mr-2" size={20} />
          Historial de Alertas
        </h3>
        {alerts.length > 0 && (
          <button 
            onClick={() => setAlerts([])}
            className="text-xs text-gray-500 bg-gray-100 px-3 py-1 rounded-full hover:bg-gray-200 transition-colors"
          >
            Limpiar todo
          </button>
        )}
      </div>
      
      {alerts.length === 0 ? (
        <div className="bg-white rounded-xl shadow-lg p-8 text-center">
          <div className="text-6xl mb-4">🌤️</div>
          <div className="text-gray-700 font-semibold text-lg mb-2">Sin alertas activas</div>
          <div className="text-gray-500 mb-4">
            {simulationActive ? 'Sistema monitoreando condiciones...' : 'Inicia el monitoreo para recibir alertas'}
          </div>
          {!simulationActive && (
            <button
              onClick={() => setSimulationActive(true)}
              className="bg-blue-600 text-white px-4 py-2 rounded-lg font-semibold hover:bg-blue-700 transition-colors"
            >
              Iniciar Monitoreo
            </button>
          )}
        </div>
      ) : (
        <div className="space-y-3">
          {alerts.map((alert, index) => {
            const alertStyle = getAlertLevel(alert.speed, alert.temperature, alert.pressure);
            return (
              <div key={alert.id} className={`bg-white rounded-xl shadow-lg p-4 border-l-4 ${alertStyle.borderColor} ${index === 0 ? 'ring-2 ring-blue-200' : ''}`}>
                <div className="flex items-start justify-between">
                  <div className="flex-1">
                    <div className="flex items-center mb-2">
                      <AlertTriangle className={`mr-2 ${alertStyle.textColor.replace('text-', 'text-')}`} size={18} />
                      <span className={`font-bold text-sm ${alertStyle.textColor}`}>
                        {alert.text}
                      </span>
                      {index === 0 && (
                        <span className="ml-2 bg-blue-600 text-white text-xs px-2 py-1 rounded-full">NUEVA</span>
                      )}
                    </div>
                    <div className="text-sm text-gray-700 mb-1">{alert.message}</div>
                    <div className="grid grid-cols-3 gap-2 text-xs text-gray-600 bg-gray-50 p-2 rounded">
                      <div>🌪️ {alert.speed} km/h</div>
                      <div>🌡️ {alert.temperature}°C</div>
                      <div>📊 {alert.pressure} hPa</div>
                    </div>
                    <div className="flex items-center justify-between mt-2">
                      <div className="text-xs text-gray-500">{alert.time}</div>
                      <div className="text-xs text-gray-500">Dirección: {alert.direction}</div>
                    </div>
                  </div>
                </div>
              </div>
            );
          })}
          
          {/* Estadísticas de alertas */}
          <div className="bg-white rounded-xl shadow-lg p-4 mt-6">
            <h4 className="font-semibold mb-3 text-gray-800">Resumen de Alertas</h4>
            <div className="grid grid-cols-3 gap-4 text-center text-sm">
              <div>
                <div className="font-bold text-red-600 text-lg">
                  {alerts.filter(a => a.level === 'rojo').length}
                </div>
                <div className="text-gray-600">Críticas</div>
              </div>
              <div>
                <div className="font-bold text-orange-600 text-lg">
                  {alerts.filter(a => a.level === 'naranja').length}
                </div>
                <div className="text-gray-600">Altas</div>
              </div>
              <div>
                <div className="font-bold text-yellow-600 text-lg">
                  {alerts.filter(a => a.level === 'amarillo').length}
                </div>
                <div className="text-gray-600">Medias</div>
              </div>
            </div>
          </div>
        </div>
      )}
    </div>
  );

  return (
    <div className="max-w-md mx-auto bg-gray-100 min-h-screen">
      {/* Header mejorado */}
      <div className="bg-gradient-to-r from-blue-600 via-blue-700 to-blue-800 text-white p-4 shadow-lg">
        <div className="flex items-center justify-between">
          <div>
            <h1 className="text-xl font-bold flex items-center">
              <Wind className="mr-2" size={24} />
              VientoSeguro
            </h1>
            <p className="text-blue-100 text-sm">Sistema de Monitoreo Meteorológico</p>
            <p className="text-blue-200 text-xs">Huancayo - Valle del Mantaro</p>
          </div>
          <div className="flex flex-col items-center space-y-1">
            <div className="flex items-center space-x-2">
              <Activity className={`${simulationActive ? 'animate-pulse text-green-300' : 'text-gray-300'}`} size={20} />
              <Settings className="text-gray-300" size={20} />
            </div>
            {simulationActive && (
              <div className="text-xs text-green-300 font-semibold">ACTIVO</div>
            )}
          </div>
        </div>
        
        {/* Indicador de estado del sistema */}
        <div className="mt-3 flex items-center justify-center">
          <div className={`w-2 h-2 rounded-full mr-2 ${simulationActive ? 'bg-green-400 animate-pulse' : 'bg-gray-400'}`}></div>
          <span className="text-xs text-blue-100">
            {simulationActive ? 'Monitoreando en tiempo real' : 'Sistema en espera'}
          </span>
        </div>
      </div>

      {/* Content */}
      <div className="pb-20">
        {activeTab === 'monitor' && <MonitorTab />}
        {activeTab === 'map' && <MapTab />}
        {activeTab === 'alerts' && <AlertsTab />}
      </div>

      {/* Bottom Navigation mejorado */}
      <div className="fixed bottom-0 left-1/2 transform -translate-x-1/2 w-full max-w-md bg-white border-t border-gray-200 shadow-lg">
        <div className="flex">
          <button
            onClick={() => setActiveTab('monitor')}
            className={`flex-1 py-3 px-4 text-center transition-all duration-200 ${
              activeTab === 'monitor' 
                ? 'text-blue-600 bg-blue-50 border-t-2 border-blue-600' 
                : 'text-gray-600 hover:text-gray-800 hover:bg-gray-50'
            }`}
          >
            <div className="relative">
              <Home className="mx-auto mb-1" size={20} />
              <div className="text-xs font-medium">Monitor</div>
              {simulationActive && activeTab === 'monitor' && (
                <div className="absolute -top-1 -right-1 w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
              )}
            </div>
          </button>
          <button
            onClick={() => setActiveTab('map')}
            className={`flex-1 py-3 px-4 text-center transition-all duration-200 ${
              activeTab === 'map' 
                ? 'text-blue-600 bg-blue-50 border-t-2 border-blue-600' 
                : 'text-gray-600 hover:text-gray-800 hover:bg-gray-50'
            }`}
          >
            <Map className="mx-auto mb-1" size={20} />
            <div className="text-xs font-medium">Mapa</div>
          </button>
          <button
            onClick={() => setActiveTab('alerts')}
            className={`flex-1 py-3 px-4 text-center relative transition-all duration-200 ${
              activeTab === 'alerts' 
                ? 'text-blue-600 bg-blue-50 border-t-2 border-blue-600' 
                : 'text-gray-600 hover:text-gray-800 hover:bg-gray-50'
            }`}
          >
            <div className="relative">
              <Bell className="mx-auto mb-1" size={20} />
              <div className="text-xs font-medium">Alertas</div>
              {alerts.length > 0 && (
                <div className="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center font-bold animate-bounce">
                  {alerts.length > 9 ? '9+' : alerts.length}
                </div>
              )}
            </div>
          </button>
        </div>
      </div>
    </div>
  );
};

export default VientoSeguroApp;
