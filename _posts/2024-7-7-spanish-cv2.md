---
title: CV_ver_jakes_1
categories: [Recruit, personal_log]
tags: [strengths, programming]
---

```LaTeX
%-------------------------
% Resume in Latex
% Author : Jake Gutierrez
% Based off of: https://github.com/sb2nov/resume
% License : MIT
%------------------------

\documentclass[letterpaper,11pt]{article}

\usepackage{latexsym}
\usepackage[empty]{fullpage}
\usepackage{titlesec}
\usepackage{marvosym}
\usepackage[usenames,dvipsnames]{color}
\usepackage{verbatim}
\usepackage{enumitem}
\usepackage[hidelinks]{hyperref}
\usepackage{fancyhdr}
\usepackage[english]{babel}
\usepackage{tabularx}
\usepackage{multicol}
\input{glyphtounicode}


%----------FONT OPTIONS----------
% sans-serif
% \usepackage[sfdefault]{FiraSans}
% \usepackage[sfdefault]{roboto}
% \usepackage[sfdefault]{noto-sans}
% \usepackage[default]{sourcesanspro}

% serif
% \usepackage{CormorantGaramond}
% \usepackage{charter}


\pagestyle{fancy}
\fancyhf{} % clear all header and footer fields
\fancyfoot{}
\renewcommand{\headrulewidth}{0pt}
\renewcommand{\footrulewidth}{0pt}

% Adjust margins
\addtolength{\oddsidemargin}{-0.5in}
\addtolength{\evensidemargin}{-0.5in}
\addtolength{\textwidth}{1in}
\addtolength{\topmargin}{-.5in}
\addtolength{\textheight}{1.0in}

\urlstyle{same}

\raggedbottom
\raggedright
\setlength{\tabcolsep}{0in}

% Sections formatting
\titleformat{\section}{
  \vspace{-4pt}\scshape\raggedright\large
}{}{0em}{}[\color{black}\titlerule \vspace{-5pt}]

% Ensure that generate pdf is machine readable/ATS parsable
\pdfgentounicode=1

%-------------------------
% Custom commands
\newcommand{\resumeItem}[1]{
  \item\small{
    {#1 \vspace{-2pt}}
  }
}

\newcommand{\resumeSubheading}[4]{
  \vspace{-2pt}\item
    \begin{tabular*}{0.97\textwidth}[t]{l@{\extracolsep{\fill}}r}
      \textbf{#1} & #2 \\
      \textit{\small#3} & \textit{\small #4} \\
    \end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeSubSubheading}[2]{
    \item
    \begin{tabular*}{0.97\textwidth}{l@{\extracolsep{\fill}}r}
      \textit{\small#1} & \textit{\small #2} \\
    \end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeProjectHeading}[2]{
    \item
    \begin{tabular*}{0.97\textwidth}{l@{\extracolsep{\fill}}r}
      \small#1 & #2 \\
    \end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeSubItem}[1]{\resumeItem{#1}\vspace{-4pt}}

\renewcommand\labelitemii{$\vcenter{\hbox{\tiny$\bullet$}}$}

\newcommand{\resumeSubHeadingListStart}{\begin{itemize}[leftmargin=0.15in, label={}]}
\newcommand{\resumeSubHeadingListEnd}{\end{itemize}}
\newcommand{\resumeItemListStart}{\begin{itemize}}
\newcommand{\resumeItemListEnd}{\end{itemize}\vspace{-5pt}}


\newcommand{\introSubHeadingListStart}{\begin{itemize}[leftmargin=0, label={}]}
\newcommand{\introSubHeadingListEnd}{\end{itemize}\vspace{-5pt}}
\newcommand{\introItemListStart}{\begin{itemize}}
\newcommand{\introItemListEnd}{\end{itemize}\vspace{-5pt}}
\newcommand{\introItem}[1]{\item #1}
%-------------------------------------------
%%%%%%  RESUME STARTS HERE  %%%%%%%%%%%%%%%%%%%%%%%%%%%%


\begin{document}

%----------HEADING----------
% \begin{tabular*}{\textwidth}{l@{\extracolsep{\fill}}r}
%   \textbf{\href{http://sourabhbajaj.com/}{\Large Sourabh Bajaj}} & Email : \href{mailto:sourabh@sourabhbajaj.com}{sourabh@sourabhbajaj.com}\\
%   \href{http://sourabhbajaj.com/}{http://www.sourabhbajaj.com} & Mobile : +1-123-456-7890 \\
% \end{tabular*}

\begin{center}
    \textbf{\Huge \scshape So Hee Park} \\ \vspace{1pt}
    \small (+34) 690 721 394 $|$
    \href{mailto:soheepark@gmail.com}{\underline{soheepark@gmail.com}} $|$
    \href{https://github.com/soheeparklee}{\underline{github.com/soheeparklee}} $|$
    \href{https://soheeparklee.github.io/}{\underline{TechBlog: soheeparklee.github.io/}}
\end{center}


%-----------Introduction-----------
\section{Introducción}
\introSubHeadingListStart
  \introItemListStart
    \introItem{Las ganas de entender los entresijos de la web y el blockchain me ha
 llevado al campo del backend.}
    \introItem{Apasionada por \textbf{el mundo de las redes} y de la \textbf{ciberseguridad}.
}
    \introItem{Interesada en trabajar en la \textbf{tecnología blockchain} y \textbf{sistemas de alto tráfico} (high-traffic systems).
}
    \introItem{Programadora con experiencia en el desarrollo de servicios para el sector educativo y personas mayores.}
    \introItem{Doy importancia a \textbf{comunicarme} con mis compañeros. Aprecio las revisiones de código para refactorizar.}
  \introItemListEnd
\introSubHeadingListEnd
%
\vspace{-\baselineskip}

%-----------PROGRAMMING SKILLS-----------
\section{FORTALEZAS}
\begin{itemize}[leftmargin=0.15in, label={}]
    \small{\item{
     \textbf{Habilidades Técnicas}{: Java, SpringBoot, IntelliJ, AWS, MySQL, Github, MariaDB, Postman} \\
     \textbf{Competencias}{: Liderazgo, Orientado a metas, Aventurero, Adaptabilidad} \\
     \textbf{Idiomas}{: Inglés (Nativo), Español (Avanzado), Coreano (Nativo)} \\
    }}
 \end{itemize}

%-------------------------------------------


%-----------PROJECTS-----------
\section{Proyectos Principales}
\resumeSubHeadingListStart

%%%%% DrugStore %%%%%
\resumeProjectHeading
    {\textbf{Aplicación Web de Cosméticos} $|$ \emph{Spring Boot, Jayspt, Nginx, EC2, RDS, Redis, Swagger}}{Mayo 2024 -- Presente}

    \resumeItemListStart
        \resumeItem{\href{https://project-movie-reservation.notion.site/DrugStore-Website-Project-d3fdec29c4d0473598382580b1416897?pvs=4}{\footnotesize\underline{\href{https://project-movie-reservation.notion.site/DrugStore-Website-Project-d3fdec29c4d0473598382580b1416897?pvs=4}{Propuesta del Proyecto}}}
        \quad \quad \quad \quad  \quad \quad \quad \quad  \raisebox{0.5ex}{\footnotesize{$\vcenter{\hbox{\tiny$\bullet$}}$}}
        \href{https://drugstoreproject-seyeons-projects-fed8a2e8.vercel.app/}{\footnotesize\underline{\href{https://drugstoreproject-seyeons-projects-fed8a2e8.vercel.app/}{Sitio Web}}}
        \quad \quad \quad \quad  \quad \quad \quad  \raisebox{0.5ex}{\footnotesize{$\vcenter{\hbox{\tiny$\bullet$}}$}}
        \href{https://drugstoreproject.shop/swagger-ui/index.html}{\footnotesize\underline{\href{https://drugstoreproject.shop/swagger-ui/index.html}{Swagger}}}
        \quad \quad \quad \quad  \quad \quad \quad \raisebox{0.5ex}{\footnotesize{$\vcenter{\hbox{\tiny$\bullet$}}$}}
        \href{https://github.com/DrugStoreWeb/DrugStore-BE.git}{\footnotesize\underline{\href{https://github.com/DrugStoreWeb/DrugStore-BE.git}{Github}}}}
        \resumeItem{Aplicación Web de cosméticos es un servicio de mercado abierto para comprar y vender productos cosméticos.}
        \resumeItem{Implementado \textbf{Jasypt} para cifrar datos confidenciales. Variables de entorno reducidas de 19 a 1.}
        \resumeItem{Configurado \textbf{Nginx, SSL, Route 53} para dominio HTTPS. Velocidad de registro de productos mejorada de 9.26s a 369ms. {\footnotesize\underline{\href{https://soheeparklee.github.io/posts/AWS_https/}{TechBlog: HTTPS}}}}
        \resumeItem{Utilizado \textbf{Redis} y Gmail \textbf{SMTP} para verificación de correo electrónico.}
        \resumeItem{Implementado \textbf{AWS S3} e\textbf{ IAM} para cargar archivos multipartes como imágenes.}
        \resumeItem{\textbf{Funcionalidad basad}\textbf{a en roles} de vendedor, comprador y administrador.}
        \resumeItem{Manejo exhaustivo de \textbf{excepciones} para posibles problemas con existencias, dinero y estado del producto.}
    \resumeItemListEnd

%%%%% Movie Reservation %%%%%
\resumeProjectHeading
    {\textbf{Reserva de Entradas de Películas}
 $|$ \emph{Spring Boot, JPA, Spring Security, Swagger}}{Abril 2024 -- Mayo 2024}

    \resumeItemListStart
        \resumeItem{\href{https://abcde}{\footnotesize\underline{Propuesta del Proyecto}}} \quad \quad \quad \quad \quad \quad \quad \quad
        \raisebox{0.5ex}{\footnotesize{$\vcenter{\hbox{\tiny$\bullet$}}$}}
        {\href{https://github.com/MovieReservationProject/MovieReservation-BE.git}{\footnotesize\underline{Github}}}
        \resumeItem{Aplicación para facilitar la reserva de entradas de películas para personas mayores.}
        \resumeItem{Desplegado en un servidor en la nube usando \textbf{AWS EC2 y RDS}.}
        \resumeItem{Implementado \textbf{Json Web Token} y \textbf{Spring Security} para registro e inicio de sesión.}
        \resumeItem{Resuelto el problema de un usuario eliminando revisiones de otras. Utilicé \textbf{JPA, List y stream} para obtener los datos apropiados.}
        \resumeItem{Estructurado \textbf{ERD }para obtener información sobre películas, horarios, cines y tipos de cines. }
        \resumeItem{\textbf{Colaboración} con 3 desarrolladores frontend y 6 backend para publicar un proyecto full-stack.}
    \resumeItemListEnd

%%%%% Thesis %%%%%
\resumeProjectHeading
    {\textbf{Tésis de Máster en Educación de Ciencias de la Computación} $|$ \href{https://m.riss.kr/link?id=T16368102}
    {\footnotesize\underline{\href{https://m.riss.kr/link?id=T16368102}{Enlace a la Tésis}}}} {Marzo 2020 -- Junio 2022}

    \begin{itemize}[leftmargin=0.15in, label={}]
        \small{\item{
        $|$ \emph{Los efectos de la Educación en Ciencia de Datos utilizando Python Coreano en el Pensamiento Computacional de los Estudiantes de Primaria}
        }}
    \end{itemize}
    \vspace{-\baselineskip}
    \resumeItemListStart
        \resumeItem{Identificada la necesidad de facilitar a estudiantes de ESL la codificación con Python usando su idioma nativo.}
        \resumeItem{Desarrollo de una herramienta para traducir código coreano a inglés, facilitando la educación en análisis de datos para estudiantes de primaria.}
        \resumeItem{Mejorado el pensamiento computacional de los estudiantes de 6.75 a 8.45 de 10 y la actitud hacia la programación de 33.7 a 36.1 de 40.}
    \resumeItemListEnd

\resumeSubHeadingListEnd
%
\vspace{-\baselineskip}

%-----------EDUCATION-----------
\section{Educación}
\resumeSubHeadingListStart
    \resumeSubheading
      {Curso de Desarrollador Backend}{Nov. 2023 -- Junio 2024}
      {Instituto Super Coding}{Madrid, remoto}
    \resumeSubheading
      {Máster en Educación de Ciencias Informáticas}{Marzo 2020 -- Junio 2022}
      {Universidad Nacional de Educación de Seúl}{Seúl, Corea}
    \resumeSubheading
      {Grado en Educación}{Marzo 2015 -- Feb. 2019}
      {Universidad Nacional de Educación de Seúl}{Seúl, Corea}
\resumeSubHeadingListEnd


%-----------Additional Experience-----------
\section{Experiencia Adicional / Liderazgo}
\resumeSubHeadingListStart
    \resumeProjectHeading
        {\textbf{Profesor de Escuela Primaria/Profesora} $|$ \emph{Escuela Primaria Sineun de Seúl, Corea}}{Marzo 2020 -- Feb. 2023}
        \resumeItemListStart
            \resumeItem{Especializada en educación en programación.}
            \resumeItem{Experiencia profesional en impartir clases de programación para niños.}
        \resumeItemListEnd
\resumeSubHeadingListEnd



%-----------EXPERIENCE-----------
% \section{Experience}
%   \resumeSubHeadingListStart

%     \resumeSubheading
%       {Undergraduate Research Assistant}{June 2020 -- Present}
%       {Texas A\&M University}{College Station, TX}
%       \resumeItemListStart
%         \resumeItem{Developed a REST API using FastAPI and PostgreSQL to store data from learning management systems}
%         \resumeItem{Developed a full-stack web application using Flask, React, PostgreSQL and Docker to analyze GitHub data}
%         \resumeItem{Explored ways to visualize GitHub collaboration in a classroom setting}
%       \resumeItemListEnd

% -----------Multiple Positions Heading-----------
%    \resumeSubSubheading
%     {Software Engineer I}{Oct 2014 - Sep 2016}
%     \resumeItemListStart
%        \resumeItem{Apache Beam}
%          {Apache Beam is a unified model for defining both batch and streaming data-parallel processing pipelines}
%     \resumeItemListEnd
%    \resumeSubHeadingListEnd
%-------------------------------------------

%     \resumeSubheading
%       {Information Technology Support Specialist}{Sep. 2018 -- Present}
%       {Southwestern University}{Georgetown, TX}
%       \resumeItemListStart
%         \resumeItem{Communicate with managers to set up campus computers used on campus}
%         \resumeItem{Assess and troubleshoot computer problems brought by students, faculty and staff}
%         \resumeItem{Maintain upkeep of computers, classroom equipment, and 200 printers across campus}
%     \resumeItemListEnd

%     \resumeSubheading
%       {Artificial Intelligence Research Assistant}{May 2019 -- July 2019}
%       {Southwestern University}{Georgetown, TX}
%       \resumeItemListStart
%         \resumeItem{Explored methods to generate video game dungeons based off of \emph{The Legend of Zelda}}
%         \resumeItem{Developed a game in Java to test the generated dungeons}
%         \resumeItem{Contributed 50K+ lines of code to an established codebase via Git}
%         \resumeItem{Conducted  a human subject study to determine which video game dungeon generation technique is enjoyable}
%         \resumeItem{Wrote an 8-page paper and gave multiple presentations on-campus}
%         \resumeItem{Presented virtually to the World Conference on Computational Intelligence}
%       \resumeItemListEnd

%   \resumeSubHeadingListEnd


\end{document}


---------how to do multicols--------
        \begin{multicols}{4}
            \begin{itemize}[itemsep=-5pt, parsep=3pt]
                \item\small Data Structures
                \item Software Methodology
                \item Algorithms Analysis
                \item Database Management
                \item Artificial Intelligence
                \item Internet Technology
                \item Systems Programming
                \item Computer Architecture
            \end{itemize}
        \end{multicols}
        \vspace*{2.0\multicolsep}





-----------한 줄 띄기--------
%\vspace{5pt}
```
