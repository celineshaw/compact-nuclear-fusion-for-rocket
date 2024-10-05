\documentclass{article}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{graphicx}

\title{Equations for 1D Particle-in-Cell Simulation}
\author{}
\date{}

\begin{document}

\maketitle

\section{Introduction}
This document outlines the key equations and concepts used in a simple one-dimensional Particle-in-Cell (PIC) simulation for plasma interactions.

\section{Key Equations}

\subsection{Charge Density Calculation}
The charge density \( \rho \) at each cell can be calculated from the particle positions as follows:
\[
\rho_j = \sum_{i=1}^{N} \frac{q}{dx} \delta(x_j - x_i)
\]
where:
\begin{itemize}
    \item \( \rho_j \) is the charge density at cell \( j \).
    \item \( q \) is the charge of each particle.
    \item \( \delta \) is the Dirac delta function that contributes to the charge density based on particle positions.
\end{itemize}

\subsection{Electric Field Calculation}
The electric field \( E \) is derived from the charge density using Gauss's law:
\[
E_j = \frac{1}{\epsilon_0} \sum_{i=1}^{N} \rho_i
\]
In a simple finite difference approximation, it can be expressed as:
\[
E_j \approx \rho_{j-1} \quad \text{(for } j > 0\text{)}
\]

\subsection{Particle Motion Update}
The velocity of each particle is updated based on the electric field:
\[
v_i(t + dt) = v_i(t) + \frac{q}{m} E_j \cdot dt
\]
where:
\begin{itemize}
    \item \( v_i \) is the velocity of particle \( i \).
    \item \( m \) is the mass of the particle.
\end{itemize}

\subsection{Position Update}
The position of each particle is updated using:
\[
x_i(t + dt) = x_i(t) + v_i(t) \cdot dt
\]

\subsection{Periodic Boundary Condition}
To ensure particles remain within the simulation domain, the positions are wrapped around:
\[
x_i = x_i \mod (L)
\]
where \( L \) is the total length of the simulation domain.

\section{Summary of the Simulation Steps}
\begin{enumerate}
    \item \textbf{Initialize Particle Positions and Velocities:} Randomly distribute particles within the simulation domain.
    \item \textbf{Calculate Charge Density:} For each particle position, update the charge density in the grid cells.
    \item \textbf{Compute Electric Field:} Use the charge density to compute the electric field at each cell.
    \item \textbf{Update Particle Velocities:} Update the velocities of particles based on the electric field.
    \item \textbf{Update Particle Positions:} Move particles based on their updated velocities, applying periodic boundary conditions.
\end{enumerate}

\end{document}
