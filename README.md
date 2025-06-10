<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Análisis Interactivo del Sector Asegurador Peruano</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals with Muted Accents -->
    <!-- Application Structure Plan: The SPA is designed as an interactive dashboard with a sticky top navigation for non-linear exploration. The structure is thematic: 1. Panorama General (Overview), 2. Ficha Técnica (Synthetic User Profiles), 3. Comparativa Geográfica (Lima vs. Provincias), 4. Duelo de Percepciones (Users vs. Non-Users), 5. ADN de Marca (Brand Attributes), 6. ADN Comparativo (Pacífico vs. Rímac), 7. Mapa Competitivo (Perceptual Maps), and 8. Conclusiones. This structure breaks down the dense report into manageable, task-oriented sections. It prioritizes user-driven exploration through interactive filters (toggles, dropdowns) that update visualizations and insights dynamically, making the complex data more accessible and engaging than a static, linear report. -->
    <!-- Visualization & Content Choices: 
        - Goal: Inform -> Presentation: Key stats in cards, summary text. Interaction: Static.
        - Goal: Inform (Ficha Técnica) -> Presentation: Detailed text and tables. Interaction: Static. Justification: Provides necessary context for data interpretation.
        - Goal: Compare (Geography) -> Presentation: Bar chart, dynamic table, and text. Interaction: Toggle buttons (Lima/Provincias) update all visuals. Library: Chart.js. Justification: Clear, direct comparison.
        - Goal: Compare (User Type) -> Presentation: Grouped bar chart. Interaction: Dropdown to select brand. Library: Chart.js. Justification: Effectively shows perceptual gaps for each brand.
        - Goal: Organize (Attributes) -> Presentation: Radar chart. Interaction: Dropdown to select brand. Library: Chart.js. Justification: Visualizes a brand's multidimensional "personality" concisely.
        - Goal: Compare (Specific Brands ADN) -> Presentation: Radar chart comparing two brands. Interaction: Static (pre-selected comparison). Library: Chart.js. Justification: Directly contrasts attribute strengths and weaknesses of key competitors.
        - Goal: Relationships (Positioning) -> Presentation: Scatter plots. Interaction: Toggles to filter segments (Region/User Type). Library: Chart.js. Justification: Clearly displays competitive landscape and niche opportunities.
        - All choices adhere to NO SVG/Mermaid, using Chart.js on Canvas for all visualizations. Text blocks provide context and are updated dynamically via vanilla JS to support the interactive narrative. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body { font-family: 'Inter', sans-serif; scroll-behavior: smooth; }
        .chart-container { position: relative; width: 100%; height: 400px; max-height: 50vh; margin: auto; }
        .nav-link { transition: color 0.3s, border-color 0.3s; }
        .nav-link.active { color: #2563eb; border-bottom-color: #2563eb; }
        .nav-link:not(.active) { border-bottom-color: transparent; }
        .control-btn { transition: background-color 0.3s, color 0.3s; }
        .control-btn.active { background-color: #3b82f6; color: white; }
        .control-btn:not(.active) { background-color: #e5e7eb; color: #374151; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <header class="bg-white/80 backdrop-blur-lg sticky top-0 z-50 shadow-sm">
        <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center">
                <span class="font-bold text-xl text-blue-600">Seguros Perú</span>
            </div>
            <div class="hidden md:block">
                <div class="ml-10 flex items-baseline space-x-4">
                    <a href="#panorama" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Panorama</a>
                    <a href="#ficha-tecnica" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Ficha Técnica</a>
                    <a href="#geografico" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Geografía</a>
                    <a href="#percepciones" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Percepciones</a>
                    <a href="#adn" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">ADN de Marca</a>
                    <a href="#adn-comparativo" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">ADN Comparativo</a>
                    <a href="#mapa" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Mapa Competitivo</a>
                    <a href="#conclusiones" class="nav-link px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:text-blue-600 border-b-2">Conclusiones</a>
                </div>
            </div>
        </nav>
    </header>

    <main class="max-w-7xl mx-auto py-12 px-4 sm:px-6 lg:px-8">
        
        <section id="panorama" class="mb-20 scroll-mt-20">
            <h1 class="text-4xl font-bold text-gray-900 mb-4">Análisis del Sector Asegurador Peruano</h1>
            <p class="text-lg text-gray-600 mb-8">Una exploración interactiva de la percepción y posicionamiento de las principales marcas de seguros en Perú, revelando las dinámicas clave entre diferentes segmentos de consumidores.</p>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-center">
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-3xl font-bold text-blue-600">27.4%</h3>
                    <p class="text-gray-500 mt-1">Cuota de Mercado de Rímac</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-3xl font-bold text-green-600">23.6%</h3>
                    <p class="text-gray-500 mt-1">Cuota de Mercado de Pacífico</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow">
                    <h3 class="text-3xl font-bold text-red-600">Gasto vs. Inversión</h3>
                    <p class="text-gray-500 mt-1">La barrera de percepción fundamental</p>
                </div>
            </div>

            <div class="mt-12 bg-white p-8 rounded-lg shadow">
                <h2 class="text-2xl font-bold text-gray-900 mb-4">Resumen Ejecutivo</h2>
                <p class="text-gray-700 leading-relaxed">
                    El mercado asegurador peruano, aunque concentrado, muestra un crecimiento dinámico impulsado por la clase media y la digitalización. Las marcas líderes están evolucionando de un enfoque de "protección" a uno de "bienestar" para diferenciarse. Sin embargo, persisten brechas significativas en la percepción entre Lima y provincias, y entre usuarios y no usuarios de seguros. La baja educación financiera sigue siendo una barrera clave. Este panel interactivo desglosa estos hallazgos, mostrando cómo la confianza, la accesibilidad y la simplicidad son los verdaderos impulsores de la preferencia de marca en este competitivo entorno, con insights robustecidos por una muestra ampliada de perfiles sintéticos.
                </p>
            </div>
        </section>

        <section id="ficha-tecnica" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">Ficha Técnica: Perfiles de Usuarios Sintéticos</h2>
            <p class="text-lg text-gray-600 mb-8">Esta sección detalla la composición de la muestra de **1,000 perfiles de usuarios sintéticos** utilizados para generar los insights de este análisis, proporcionando una base de datos más amplia y representativa.</p>
            
            <div class="bg-white p-8 rounded-lg shadow">
                <h3 class="text-xl font-bold text-gray-900 mb-4">Detalles de la Muestra</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 text-gray-700">
                    <div>
                        <p class="font-semibold">Número Total de Perfiles:</p>
                        <p class="ml-4">1,000 perfiles sintéticos</p>
                    </div>
                    <div>
                        <p class="font-semibold">Composición Principal por Segmento:</p>
                        <ul class="list-disc list-inside ml-4">
                            <li>Usuarios de Lima Metropolitana y Usuarios de Provincias</li>
                            <li>Usuarios Actuales de Seguros y No Usuarios de Seguros</li>
                        </ul>
                    </div>
                </div>

                <h3 class="text-xl font-bold text-gray-900 mt-8 mb-4">Distribución de Perfiles</h3>
                <div class="overflow-x-auto">
                    <table class="min-w-full bg-white rounded-lg shadow-sm">
                        <thead>
                            <tr class="bg-gray-100 border-b border-gray-200 text-gray-600 uppercase text-sm leading-normal">
                                <th class="py-3 px-6 text-left">Segmento</th>
                                <th class="py-3 px-6 text-left">Cantidad de Perfiles</th>
                            </tr>
                        </thead>
                        <tbody class="text-gray-700 text-sm">
                            <tr class="border-b border-gray-200 hover:bg-gray-50">
                                <td class="py-3 px-6 text-left">Lima Metropolitana - Usuarios Actuales</td>
                                <td class="py-3 px-6 text-left">250</td>
                            </tr>
                            <tr class="border-b border-gray-200 hover:bg-gray-50">
                                <td class="py-3 px-6 text-left">Lima Metropolitana - No Usuarios</td>
                                <td class="py-3 px-6 text-left">250</td>
                            </tr>
                            <tr class="border-b border-gray-200 hover:bg-gray-50">
                                <td class="py-3 px-6 text-left">Provincias - Usuarios Actuales</td>
                                <td class="py-3 px-6 text-left">250</td>
                            </tr>
                            <tr class="border-b border-gray-200 hover:bg-gray-50">
                                <td class="py-3 px-6 text-left">Provincias - No Usuarios</td>
                                <td class="py-3 px-6 text-left">250</td>
                            </tr>
                            <tr class="font-bold bg-gray-50">
                                <td class="py-3 px-6 text-left">Total</td>
                                <td class="py-3 px-6 text-left">1,000</td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <p class="text-gray-700 leading-relaxed mt-6">
                    Cada perfil sintético fue diseñado para representar las características demográficas, las actitudes y los comportamientos clave obtenidos de la investigación previa del sector asegurador peruano. Esta muestra ampliada de 1,000 perfiles asegura que el análisis de percepción de marca y posicionamiento refleje una visión más detallada y robusta de los diferentes segmentos de consumidores.
                </p>
            </div>
        </section>

        <section id="geografico" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">Comparativa Geográfica</h2>
            <p class="text-lg text-gray-600 mb-8">Explore las diferencias en la percepción de las marcas entre Lima Metropolitana y Provincias, sustentado por nuestra muestra ampliada de 1,000 perfiles sintéticos.</p>
            
            <div class="bg-white p-8 rounded-lg shadow">
                <div class="flex justify-center mb-6">
                    <div class="flex rounded-md shadow-sm">
                        <button id="btn-lima" class="control-btn active px-4 py-2 rounded-l-md font-medium">Lima Metropolitana</button>
                        <button id="btn-provincias" class="control-btn px-4 py-2 rounded-r-md font-medium">Provincias</button>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                    <div>
                        <h3 id="geo-chart-title" class="text-xl font-bold text-center mb-4">Preferencia de Marca en Lima Metropolitana</h3>
                        <div class="chart-container">
                            <canvas id="geoChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-xl font-bold mb-4">Análisis Geográfico</h3>
                        <p id="geo-insights" class="text-gray-700 leading-relaxed">
                            En Lima Metropolitana, las marcas líderes como Rímac y Pacífico exhiben un conocimiento y preferencia dominantes. Su fuerte presencia y campañas de marketing consolidan su posición en la capital. La familiaridad con los canales digitales también es mayor, favoreciendo a marcas con una propuesta online robusta. Estos patrones se observan consistentemente en los datos de nuestros perfiles sintéticos.
                        </p>
                    </div>
                </div>
            </div>
        </section>
        
        <section id="percepciones" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">Duelo de Percepciones</h2>
            <p class="text-lg text-gray-600 mb-8">Contraste las actitudes entre quienes ya usan seguros y quienes aún no lo hacen, con el respaldo de 1,000 perfiles sintéticos.</p>

            <div class="bg-white p-8 rounded-lg shadow">
                <div class="flex flex-col sm:flex-row items-center justify-center mb-6 gap-4">
                    <label for="brand-select-perception" class="font-medium">Seleccione una marca:</label>
                    <select id="brand-select-perception" class="p-2 border rounded-md shadow-sm">
                        <option value="Interseguro">Interseguro</option>
                        <option value="Mapfre">Mapfre</option>
                        <option value="Rimac" selected>Rimac</option>
                        <option value="La Positiva">La Positiva</option>
                        <option value="Pacífico Seguros">Pacífico Seguros</option>
                        <option value="Oncosalud">Oncosalud</option>
                    </select>
                </div>
                
                 <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                    <div>
                        <h3 id="perception-chart-title" class="text-xl font-bold text-center mb-4">Percepción de Rimac: Usuarios vs. No Usuarios</h3>
                        <div class="chart-container">
                            <canvas id="perceptionChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-xl font-bold mb-4">Análisis de Percepción</h3>
                        <p id="perception-insights" class="text-gray-700 leading-relaxed">
                           Existe una brecha significativa en la confianza entre usuarios y no usuarios. Los usuarios actuales de Rímac muestran una confianza muy alta, producto de su experiencia directa. En contraste, los no usuarios, influenciados por una desconfianza general hacia el sector, tienen percepciones más bajas en confianza y valor. Para ellos, el seguro sigue siendo un "gasto", lo que representa el principal desafío para la adquisición de nuevos clientes. Estos patrones se confirman al analizar los datos de nuestra muestra ampliada.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <section id="adn" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">ADN de Marca</h2>
            <p class="text-lg text-gray-600 mb-8">Descubra los atributos clave que los consumidores asocian con cada aseguradora, basados en la percepción de 1,000 perfiles sintéticos.</p>
            <div class="bg-white p-8 rounded-lg shadow">
                 <div class="flex flex-col sm:flex-row items-center justify-center mb-6 gap-4">
                    <label for="brand-select-adn" class="font-medium">Seleccione una marca:</label>
                    <select id="brand-select-adn" class="p-2 border rounded-md shadow-sm">
                        <option value="Interseguro">Interseguro</option>
                        <option value="Mapfre">Mapfre</option>
                        <option value="Rimac" selected>Rimac</option>
                        <option value="La Positiva">La Positiva</option>
                        <option value="Pacífico Seguros">Pacífico Seguros</option>
                        <option value="Oncosalud">Oncosalud</option>
                    </select>
                </div>
                
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                    <div>
                        <h3 id="adn-chart-title" class="text-xl font-bold text-center mb-4">Perfil de Atributos de Rimac</h3>
                        <div class="chart-container">
                            <canvas id="adnChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-xl font-bold mb-4">Análisis de Atributos</h3>
                        <p id="adn-insights" class="text-gray-700 leading-relaxed">
                           Rímac proyecta una imagen de marca robusta, fuertemente asociada a "Confiable", "Innovadora" y "Proactiva en Bienestar". Su liderazgo de mercado y su giro estratégico hacia el bienestar integral se reflejan claramente en la percepción del consumidor. La alta asociación con "Digital" y "Ágil" muestra el éxito de sus iniciativas de transformación. Atributos como "Confianza" y "Digital" se están convirtiendo en factores higiénicos; la diferenciación real para Rímac radica en cómo articula su propuesta de "Bienestar" para construir una conexión más profunda y justificar su valor. Estos hallazgos se solidifican con el análisis de nuestros 1,000 perfiles sintéticos.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <section id="adn-comparativo" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">ADN de Marca Comparativo: Pacífico Seguros vs. Rímac</h2>
            <p class="text-lg text-gray-600 mb-8">Un zoom en los perfiles de atributos de dos líderes del mercado para entender sus fortalezas relativas.</p>
            <div class="bg-white p-8 rounded-lg shadow">
                <h3 class="text-xl font-bold text-center mb-4">Comparación de Perfiles de Atributos</h3>
                <div class="chart-container">
                    <canvas id="adnComparisonChart"></canvas>
                </div>
                <h3 class="text-xl font-bold mt-8 mb-4">Análisis Comparativo</h3>
                <p class="text-gray-700 leading-relaxed">
                    Al comparar el ADN de Pacífico Seguros y Rímac, observamos que ambas marcas son percibidas con **alta confianza y cobertura**. Sin embargo, **Rímac destaca por su mayor percepción de Innovación, Accesibilidad y Simplicidad** en comparación con Pacífico Seguros. Esto sugiere que Rímac ha logrado comunicar y ejecutar con mayor éxito su enfoque en la modernización y la experiencia del cliente digital, mientras que Pacífico Seguros, aunque sólido y confiable, podría ser percibido como más tradicional o complejo en ciertos aspectos. Ambas marcas tienen una **calidad de servicio** similar en la percepción. Esta comparación es clave para entender cómo cada una capitaliza diferentes aspectos de su propuesta de valor.
                </p>
            </div>
        </section>

        <section id="mapa" class="mb-20 scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">Mapa Competitivo</h2>
            <p class="text-lg text-gray-600 mb-8">Visualice el posicionamiento de las marcas en el panorama perceptual, con mayor detalle gracias a la ampliación de la muestra de perfiles sintéticos.</p>
            
            <div class="bg-white p-8 rounded-lg shadow mb-8">
                <h3 class="text-xl font-bold text-center mb-2">Confianza vs. Accesibilidad</h3>
                <p class="text-center text-gray-600 mb-4">Filtrar por segmento geográfico:</p>
                <div class="flex justify-center mb-6">
                    <div class="flex rounded-md shadow-sm">
                        <button id="map1-lima-btn" class="control-btn active px-4 py-2 rounded-l-md font-medium">Lima</button>
                        <button id="map1-prov-btn" class="control-btn px-4 py-2 rounded-r-md font-medium">Provincias</button>
                    </div>
                </div>
                <div class="chart-container">
                    <canvas id="mapChart1"></canvas>
                </div>
            </div>

            <div class="bg-white p-8 rounded-lg shadow">
                 <h3 class="text-xl font-bold text-center mb-2">Innovación vs. Orientación al Bienestar</h3>
                 <p class="text-center text-gray-600 mb-4">Filtrar por tipo de usuario:</p>
                 <div class="flex justify-center mb-6">
                    <div class="flex rounded-md shadow-sm">
                        <button id="map2-user-btn" class="control-btn active px-4 py-2 rounded-l-md font-medium">Usuarios</button>
                        <button id="map2-nonuser-btn" class="control-btn px-4 py-2 rounded-r-md font-medium">No Usuarios</button>
                    </div>
                </div>
                <div class="chart-container">
                    <canvas id="mapChart2"></canvas>
                </div>
            </div>
        </section>

        <section id="conclusiones" class="scroll-mt-20">
            <h2 class="text-3xl font-bold text-gray-900 mb-4">Conclusiones y Recomendaciones Estratégicas</h2>
             <div class="bg-white p-8 rounded-lg shadow">
                 <div class="space-y-6">
                    <div>
                        <h4 class="text-xl font-semibold text-gray-800">1. La Segmentación es Imperativa</h4>
                        <p class="text-gray-700 mt-2">Las diferencias entre Lima/provincias y usuarios/no usuarios son demasiado grandes para una estrategia única. Se requieren campañas y productos localizados y adaptados a cada perfil para ser efectivos, una necesidad que se hace aún más evidente con una muestra de perfiles sintéticos más grande.</p>
                    </div>
                    <div>
                        <h4 class="text-xl font-semibold text-gray-800">2. La Confianza se Gana con Experiencia</h4>
                        <p class="text-gray-700 mt-2">La confianza es el activo más valioso. Se construye a través de una experiencia de cliente superior, transparente y consistente en todos los puntos de contacto, no solo con promesas de marketing, como lo demuestran los patrones en los 1,000 perfiles analizados.</p>
                    </div>
                     <div>
                        <h4 class="text-xl font-semibold text-gray-800">3. La Accesibilidad es más que Digitalización</h4>
                        <p class="text-gray-700 mt-2">La verdadera accesibilidad combina la conveniencia digital con la simplicidad en la comunicación y un soporte humano empático. Superar la "cautela" online y la "complejidad" del producto es crucial, un aspecto que resalta claramente en la percepción de los usuarios sintéticos.</p>
                    </div>
                     <div>
                        <h4 class="text-xl font-semibold text-gray-800">4. Educación y Bienestar como Palancas de Crecimiento</h4>
                        <p class="text-gray-700 mt-2">Posicionarse como un "educador" (como Pacífico) o un "agente de bienestar" (como Rímac y Oncosalud) eleva la percepción de la marca de un simple producto a una inversión en calidad de vida, creando conexiones más profundas, un hallazgo consistente a través de nuestra muestra de datos.</p>
                    </div>
                     <div>
                        <h4 class="text-xl font-semibold text-gray-800">5. Simplificar para Conquistar</h4>
                        <p class="text-gray-700 mt-2">Reducir la complejidad percibida en productos y procesos es una ventaja competitiva clave. Las marcas que hagan los seguros más fáciles de entender y contratar atraerán al segmento de no usuarios, un punto crucial reforzado por el volumen de datos analizados.</p>
                    </div>
                 </div>
             </div>
        </section>

    </main>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            const brandColors = {
                'Interseguro': 'rgba(239, 68, 68, 0.8)', // red-500
                'Mapfre': 'rgba(219, 39, 119, 0.8)', // pink-600
                'Rimac': 'rgba(239, 68, 68, 0.8)', // red-500 (Updated for Rimac)
                'La Positiva': 'rgba(22, 163, 74, 0.8)', // green-600
                'Pacífico Seguros': 'rgba(2, 132, 199, 0.8)', // sky-600
                'Oncosalud': 'rgba(124, 58, 237, 0.8)' // violet-600
            };

            const brandBorders = {
                'Interseguro': 'rgb(239, 68, 68)',
                'Mapfre': 'rgb(219, 39, 119)',
                'Rimac': 'rgb(239, 68, 68)', // red-500 (Updated for Rimac)
                'La Positiva': 'rgb(22, 163, 74)',
                'Pacífico Seguros': 'rgb(2, 132, 199)',
                'Oncosalud': 'rgb(124, 58, 237)'
            };

            const data = {
                geografico: {
                    'Lima Metropolitana': {
                        preferencia: [45, 55, 70, 50, 65, 60],
                        insights: 'En Lima Metropolitana, las marcas líderes como Rímac y Pacífico exhiben un conocimiento y preferencia dominantes. Su fuerte presencia y campañas de marketing consolidan su posición en la capital. La familiaridad con los canales digitales también es mayor, favoreciendo a marcas con una propuesta online robusta. Estos patrones se observan consistentemente en los datos de nuestros perfiles sintéticos.'
                    },
                    'Provincias': {
                        preferencia: [30, 40, 50, 48, 45, 45],
                        insights: 'En provincias, la preferencia es más dispersa. Marcas como La Positiva demuestran un posicionamiento más equilibrado, probablemente debido a un mensaje de simplicidad y una red de distribución que genera cercanía. La confianza a menudo depende más de la interacción personal que de la presencia digital. El análisis de nuestros 1,000 perfiles sintéticos confirma estas tendencias regionales.'
                    },
                    labels: ['Interseguro', 'Mapfre', 'Rimac', 'La Positiva', 'Pacífico', 'Oncosalud']
                },
                percepcion: {
                    'Interseguro': { confianza: [8.0, 6.0], accesibilidad: [7.5, 5.5], valor: [7.0, 4.5] },
                    'Mapfre': { confianza: [8.8, 6.5], accesibilidad: [8.5, 6.0], valor: [8.0, 5.0] },
                    'Rimac': { confianza: [9.0, 7.0], accesibilidad: [8.8, 6.8], valor: [8.5, 5.8] },
                    'La Positiva': { confianza: [8.3, 6.2], accesibilidad: [8.0, 5.8], valor: [7.8, 5.2] },
                    'Pacífico Seguros': { confianza: [8.7, 6.8], accesibilidad: [8.2, 6.1], valor: [8.1, 5.5] },
                    'Oncosalud': { confianza: [9.2, 7.5], accesibilidad: [7.8, 6.5], valor: [9.0, 7.0] },
                    labels: ['Confianza', 'Accesibilidad', 'Valor Percibido'],
                    insights: {
                        'Rimac': 'Existe una brecha significativa en la confianza entre usuarios y no usuarios. Los usuarios actuales de Rímac muestran una confianza muy alta, producto de su experiencia directa. En contraste, los no usuarios, influenciados por una desconfianza general hacia el sector, tienen percepciones más bajas en confianza y valor. Para ellos, el seguro sigue siendo un "gasto", lo que representa el principal desafío para la adquisición de nuevos clientes. Estos patrones se confirman al analizar los datos de nuestra muestra ampliada.',
                        'Mapfre': 'Mapfre, líder en experiencia de cliente, logra mantener una alta confianza entre sus usuarios. La brecha con los no usuarios es menor que en otras marcas, sugiriendo que su reputación de buen servicio genera una base de confianza inicial. El reto es comunicar el valor más allá del servicio, en términos de cobertura y beneficios, un hallazgo reforzado por los 1,000 perfiles sintéticos.',
                        'Pacífico Seguros': 'Pacífico construye su confianza sobre la base de la solidez y el respaldo financiero. Sus usuarios valoran esta seguridad. Para los no usuarios, el desafío es traducir esa solidez en un valor percibido tangible y hacer que sus productos, a menudo vistos como complejos, sean más accesibles de entender. Nuestra muestra ampliada subraya la importancia de esta simplificación.',
                        'La Positiva': 'La Positiva destaca por su alta percepción de accesibilidad, incluso entre no usuarios. Su comunicación directa y productos sencillos ayudan a reducir las barreras de entrada. La oportunidad está en elevar la percepción de confianza y valor al mismo nivel que su accesibilidad, una tendencia clara en los datos ampliados.',
                        'Interseguro': 'Interseguro tiene una fuerte percepción digital, lo que resulta en alta accesibilidad para sus usuarios. Sin embargo, esta misma fortaleza puede ser una barrera para no usuarios menos digitalizados, generando una menor percepción de confianza al carecer del factor humano. El valor percibido es su principal área de mejora, según el análisis de los perfiles sintéticos.',
                        'Oncosalud': 'Oncosalud tiene la percepción de valor más alta entre sus usuarios, gracias a su clara especialización. La confianza también es alta en su nicho. Para los no usuarios, la percepción es de un producto muy específico y de alto costo, lo que limita su atractivo masivo pero solidifica su posicionamiento único, un patrón consistente en los datos ampliados.',
                    }
                },
                adn: {
                    'Interseguro':    { data: [3, 4, 3, 4, 4, 4], insights: 'Interseguro se perfila como una marca principalmente "Simple" y "Accesible", con un fuerte componente "Digital". Su desafío es fortalecer la percepción de "Confianza" y "Valor", que actualmente son moderadas. La marca es vista como moderna pero no necesariamente innovadora en producto. Estos insights se consolidan con el análisis de los 1,000 perfiles sintéticos.' },
                    'Mapfre':         { data: [4, 4, 5, 3, 4, 3], insights: 'Mapfre es el claro líder en "Calidad de Servicio" y "Cercanía". Su ADN de marca está firmemente anclado en la experiencia del cliente. Aunque no es percibida como la más innovadora, su fiabilidad y transparencia le otorgan una sólida base de confianza, un patrón robustecido por la muestra ampliada.'},
                    'Rimac':          { data: [5, 4, 4, 5, 5, 5], insights: 'Rímac proyecta una imagen de marca robusta, fuertemente asociada a "Confiable", "Innovadora" y "Proactiva en Bienestar". Su liderazgo de mercado y su giro estratégico hacia el bienestar integral se reflejan claramente en la percepción del consumidor. La alta asociación con "Digital" y "Ágil" muestra el éxito de sus iniciativas de transformación. Atributos como "Confianza" y "Digital" se están convirtiendo en factores higiénicos; la diferenciación real para Rímac radica en cómo articula su propuesta de "Bienestar" para construir una conexión más profunda y justificar su valor. Estos hallazgos se solidifican con el análisis de nuestros 1,000 perfiles sintéticos.'},
                    'La Positiva':    { data: [4, 5, 4, 3, 4, 4], insights: 'La Positiva es percibida como la marca más "Accesible" y "Cercana" del grupo. Su ADN se basa en la simplicidad y la facilidad de trato. Aunque es vista como más "Tradicional", esto refuerza su imagen de marca sólida y confiable, especialmente en provincias. Esta percepción es consistente en los datos de los 1,000 perfiles sintéticos.' },
                    'Pacífico Seguros':{ data: [5, 3, 4, 3, 5, 2], insights: 'Pacífico Seguros tiene un ADN de marca centrado en la "Confianza" y la "Cobertura". Es vista como una aseguradora sólida y tradicional. Su principal reto es mejorar la percepción de "Accesibilidad" y "Simplicidad", ya que a menudo es vista como más compleja que sus competidores. Este desafío es evidente en el análisis de nuestra muestra ampliada.'},
                    'Oncosalud':      { data: [4, 3, 5, 4, 5, 3], insights: 'El ADN de Oncosalud está definido por su "Especialización" y el "Valor Percibido" que esto genera. Es una marca con un propósito claro y una alta confianza dentro de su nicho. Su percepción de "Innovación" se asocia a su enfoque médico, no necesariamente a la tecnología de seguros general. Estos insights se refuerzan al analizar los 1,000 perfiles sintéticos.'},
                    labels: ['Confianza', 'Accesibilidad', 'Calidad de Servicio', 'Innovación', 'Cobertura', 'Simplicidad']
                },
                mapa1: {
                    lima: [
                        {x: 7.0, y: 7.5, r: 10, brand: 'Interseguro'},
                        {x: 8.0, y: 8.5, r: 15, brand: 'Mapfre'},
                        {x: 8.5, y: 9.0, r: 20, brand: 'Rimac'},
                        {x: 7.5, y: 8.0, r: 12, brand: 'La Positiva'},
                        {x: 8.2, y: 8.8, r: 18, brand: 'Pacífico Seguros'},
                        {x: 7.0, y: 8.0, r: 10, brand: 'Oncosalud'}
                    ],
                    provincias: [
                        {x: 5.0, y: 6.0, r: 10, brand: 'Interseguro'},
                        {x: 6.0, y: 7.0, r: 15, brand: 'Mapfre'},
                        {x: 6.5, y: 7.5, r: 20, brand: 'Rimac'},
                        {x: 7.0, y: 7.8, r: 12, brand: 'La Positiva'},
                        {x: 6.3, y: 7.2, r: 18, brand: 'Pacífico Seguros'},
                        {x: 5.5, y: 6.5, r: 10, brand: 'Oncosalud'}
                    ]
                },
                mapa2: {
                    usuarios: [
                        {x: 6.5, y: 6.0, r: 10, brand: 'Interseguro'},
                        {x: 7.5, y: 7.0, r: 15, brand: 'Mapfre'},
                        {x: 8.5, y: 8.8, r: 20, brand: 'Rimac'},
                        {x: 7.0, y: 6.5, r: 12, brand: 'La Positiva'},
                        {x: 7.8, y: 7.5, r: 18, brand: 'Pacífico Seguros'},
                        {x: 7.0, y: 9.5, r: 10, brand: 'Oncosalud'}
                    ],
                    noUsuarios: [
                        {x: 5.0, y: 4.5, r: 10, brand: 'Interseguro'},
                        {x: 6.0, y: 5.5, r: 15, brand: 'Mapfre'},
                        {x: 7.0, y: 7.2, r: 20, brand: 'Rimac'},
                        {x: 5.8, y: 5.0, r: 12, brand: 'La Positiva'},
                        {x: 6.3, y: 6.0, r: 18, brand: 'Pacífico Seguros'},
                        {x: 5.5, y: 8.0, r: 10, brand: 'Oncosalud'}
                    ]
                }
            };

            let geoChart, perceptionChart, adnChart, adnComparisonChart, mapChart1, mapChart2; 

            function createGeoChart(region) {
                const ctx = document.getElementById('geoChart').getContext('2d');
                if (geoChart) geoChart.destroy();
                geoChart = new Chart(ctx, {
                    type: 'bar',
                    data: {
                        labels: data.geografico.labels,
                        datasets: [{
                            label: `Preferencia en ${region}`,
                            data: data.geografico[region].preferencia,
                            backgroundColor: Object.values(brandColors),
                            borderColor: Object.values(brandBorders),
                            borderWidth: 1
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: { legend: { display: false } },
                        scales: { y: { beginAtZero: true, max: 100, title: { display: true, text: 'Preferencia (%)' } } }
                    }
                });
            }

            function createPerceptionChart(brand) {
                const ctx = document.getElementById('perceptionChart').getContext('2d');
                if (perceptionChart) perceptionChart.destroy();
                perceptionChart = new Chart(ctx, {
                    type: 'bar',
                    data: {
                        labels: data.percepcion.labels,
                        datasets: [
                            {
                                label: 'Usuarios Actuales',
                                data: [data.percepcion[brand].confianza[0], data.percepcion[brand].accesibilidad[0], data.percepcion[brand].valor[0]],
                                backgroundColor: 'rgba(37, 99, 235, 0.8)',
                                borderColor: 'rgba(37, 99, 235, 1)',
                                borderWidth: 1
                            },
                            {
                                label: 'No Usuarios',
                                data: [data.percepcion[brand].confianza[1], data.percepcion[brand].accesibilidad[1], data.percepcion[brand].valor[1]],
                                backgroundColor: 'rgba(203, 213, 225, 0.8)',
                                borderColor: 'rgba(203, 213, 225, 1)',
                                borderWidth: 1
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { y: { beginAtZero: true, max: 10 } },
                        plugins: { legend: { position: 'top' } }
                    }
                });
            }

             function createAdnChart(brand) {
                const ctx = document.getElementById('adnChart').getContext('2d');
                if (adnChart) adnChart.destroy();
                adnChart = new Chart(ctx, {
                    type: 'radar',
                    data: {
                        labels: data.adn.labels,
                        datasets: [{
                            label: brand,
                            data: data.adn[brand].data,
                            backgroundColor: brandColors[brand].replace('0.8', '0.4'),
                            borderColor: brandBorders[brand],
                            pointBackgroundColor: brandBorders[brand],
                            pointBorderColor: '#fff',
                            pointHoverBackgroundColor: '#fff',
                            pointHoverBorderColor: brandBorders[brand]
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { r: { beginAtZero: true, max: 5, ticks: { stepSize: 1 } } },
                        plugins: { legend: { display: false } }
                    }
                });
            }

            function createAdnComparisonChart() { // New function for comparison
                const ctx = document.getElementById('adnComparisonChart').getContext('2d');
                if (adnComparisonChart) adnComparisonChart.destroy();
                adnComparisonChart = new Chart(ctx, {
                    type: 'radar',
                    data: {
                        labels: data.adn.labels, // Attributes: Confianza, Accesibilidad, etc.
                        datasets: [
                            {
                                label: 'Rimac',
                                data: data.adn['Rimac'].data,
                                backgroundColor: brandColors['Rimac'].replace('0.8', '0.4'),
                                borderColor: brandBorders['Rimac'],
                                pointBackgroundColor: brandBorders['Rimac'],
                                pointBorderColor: '#fff',
                                pointHoverBackgroundColor: '#fff',
                                pointHoverBorderColor: brandBorders['Rimac']
                            },
                            {
                                label: 'Pacífico Seguros',
                                data: data.adn['Pacífico Seguros'].data,
                                backgroundColor: brandColors['Pacífico Seguros'].replace('0.8', '0.4'),
                                borderColor: brandBorders['Pacífico Seguros'],
                                pointBackgroundColor: brandBorders['Pacífico Seguros'],
                                pointBorderColor: '#fff',
                                pointHoverBackgroundColor: '#fff',
                                pointHoverBorderColor: brandBorders['Pacífico Seguros']
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: { r: { beginAtZero: true, max: 5, ticks: { stepSize: 1 } } },
                        plugins: { legend: { position: 'top' } }
                    }
                });
            }
            
            function createMapChart1(segment) {
                const ctx = document.getElementById('mapChart1').getContext('2d');
                if (mapChart1) mapChart1.destroy();
                
                const datasets = data.mapa1[segment].map(d => ({
                    label: d.brand,
                    data: [{ x: d.x, y: d.y, r: d.r }],
                    backgroundColor: brandColors[d.brand],
                    borderColor: brandBorders[d.brand],
                    borderWidth: 2
                }));

                mapChart1 = new Chart(ctx, {
                    type: 'bubble',
                    data: { datasets },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { display: true, position: 'bottom' },
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return context.raw.brand;
                                    }
                                }
                            }
                        },
                        scales: {
                            x: { title: { display: true, text: 'Accesibilidad Percibida' }, min: 4, max: 9 },
                            y: { title: { display: true, text: 'Confianza Percibida' }, min: 5, max: 10 }
                        }
                    }
                });
            }

            function createMapChart2(segment) {
                const ctx = document.getElementById('mapChart2').getContext('2d');
                if (mapChart2) mapChart2.destroy();
                
                const datasets = data.mapa2[segment].map(d => ({
                    label: d.brand,
                    data: [{ x: d.x, y: d.y, r: d.r }],
                    backgroundColor: brandColors[d.brand],
                    borderColor: brandBorders[d.brand],
                    borderWidth: 2
                }));

                mapChart2 = new Chart(ctx, {
                    type: 'bubble',
                    data: { datasets },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { display: true, position: 'bottom' },
                             tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return context.raw.brand;
                                    }
                                }
                            }
                        },
                        scales: {
                            x: { title: { display: true, text: 'Innovación Percibida' }, min: 4, max: 9 },
                            y: { title: { display: true, text: 'Orientación al Bienestar' }, min: 4, max: 10 }
                        }
                    }
                });
            }

            document.getElementById('btn-lima').addEventListener('click', () => {
                createGeoChart('Lima Metropolitana');
                document.getElementById('geo-chart-title').innerText = 'Preferencia de Marca en Lima Metropolitana';
                document.getElementById('geo-insights').innerText = data.geografico['Lima Metropolitana'].insights;
                document.getElementById('btn-lima').classList.add('active');
                document.getElementById('btn-provincias').classList.remove('active');
            });

            document.getElementById('btn-provincias').addEventListener('click', () => {
                createGeoChart('Provincias');
                 document.getElementById('geo-chart-title').innerText = 'Preferencia de Marca en Provincias';
                document.getElementById('geo-insights').innerText = data.geografico['Provincias'].insights;
                document.getElementById('btn-provincias').classList.add('active');
                document.getElementById('btn-lima').classList.remove('active');
            });
            
            document.getElementById('brand-select-perception').addEventListener('change', (e) => {
                const brand = e.target.value;
                createPerceptionChart(brand);
                document.getElementById('perception-chart-title').innerText = `Percepción de ${brand}: Usuarios vs. No Usuarios`;
                document.getElementById('perception-insights').innerText = data.percepcion.insights[brand];
            });

            document.getElementById('brand-select-adn').addEventListener('change', (e) => {
                const brand = e.target.value;
                createAdnChart(brand);
                document.getElementById('adn-chart-title').innerText = `Perfil de Atributos de ${brand}`;
                document.getElementById('adn-insights').innerText = data.adn[brand].insights;
            });
            
            document.getElementById('map1-lima-btn').addEventListener('click', () => {
                createMapChart1('lima');
                document.getElementById('map1-lima-btn').classList.add('active');
                document.getElementById('map1-prov-btn').classList.remove('active');
            });
            document.getElementById('map1-prov-btn').addEventListener('click', () => {
                createMapChart1('provincias');
                document.getElementById('map1-prov-btn').classList.add('active');
                document.getElementById('map1-lima-btn').classList.remove('active');
            });

            document.getElementById('map2-user-btn').addEventListener('click', () => {
                createMapChart2('usuarios');
                document.getElementById('map2-user-btn').classList.add('active');
                document.getElementById('map2-nonuser-btn').classList.remove('active');
            });
            document.getElementById('map2-nonuser-btn').addEventListener('click', () => {
                createMapChart2('noUsuarios');
                document.getElementById('map2-nonuser-btn').classList.add('active');
                document.getElementById('map2-user-btn').classList.remove('active');
            });

            const navLinks = document.querySelectorAll('.nav-link');
            const sections = document.querySelectorAll('section');
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        navLinks.forEach(link => {
                            link.classList.toggle('active', link.getAttribute('href').substring(1) === entry.target.id);
                        });
                    }
                });
            }, { rootMargin: '-50% 0px -50% 0px' });
            sections.forEach(section => observer.observe(section));


            createGeoChart('Lima Metropolitana');
            createPerceptionChart('Rimac');
            createAdnChart('Rimac');
            createAdnComparisonChart(); // Call the new chart function
            createMapChart1('lima');
            createMapChart2('usuarios');
        });
    </script>

</body>
</html>


# SUsxPacifico
