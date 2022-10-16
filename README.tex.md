\documentclass{article}[12pt]
\usepackage{fullpage}
\usepackage[ruled,lined,linesnumbered]{algorithm2e}
\usepackage{algpseudocode}
\usepackage{multicol}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{amsthm}
\usepackage{amssymb}
\usepackage{enumitem}
\usepackage{url}
\usepackage{graphicx}
\usepackage{listings}
\usepackage{subcaption}

\title{CS205, Artificial Intelligence, Dr. Eamonn Keogh \\ The Eight Puzzle}
\author{Md Rayhanul Masud (SID: 862317259) \\ Email {mmasu012@ucr.edu} }
\date{May 13 2022}

\begin{document}

\maketitle
\ 
\\
\textbf{References} The references that I have followed to complete the assignment
\begin{itemize}
    \item The lecture contents related to the Blind Search and Heuristic Search topics
    \item Documentation of Python 3.10 https://docs.python.org/3
    \item The description of the project
    \item The attached sample report of the project description
\end{itemize}
 
\ 
\\
\textbf{Code Implementation} The python code implementation of this project is solely original except the library/packages from python
\begin{itemize}
    \item \textbf{heapq} to maintain a priority queue for the list of Eight Puzzle board states based on 3 different heuristics
    \item \textbf{deepcopy} to generate new board state
    \item \textbf{time} to calculate the execution time needed to run the code
    \item \textbf{matplotlib} to generate plots/figures to describe the comparisons identified among the 3 different heuristics to search for a solution of the given problem 
\end{itemize}
\ 
\\
\textbf{Outline of the report} 
\begin{itemize}
    \item Cover Page (Page 1)
    \item The description of 3 different heuristics (Page 2 to Page 6)
    \item The sample trace of a search (over the test cases) with the source code implementation (At the end of the report)
    \item The source code is also upload in https://github.com/mmasu012/Eight-Puzzle
\end{itemize}

\newpage 

\section{Introduction}
\subsection{What is the Eight Puzzle}
The Eight Puzzle is a puzzle where an orientation of 8 tiles numbering from 1-8 placed in a 3*3 matrix is given, and the puzzle solver needs to turn the orientation into a specific/given orientation called Goal state to solve the puzzle, by a series of sliding the tiles to the next possible empty blank position in the matrix. 
\ \\ \\
This project is aimed to implement 3 known heuristics: Uniform Cost Search, $A^{*}$ search with Misplaced Tiles and $A^{*}$ search with Manhattan Distance to solve the puzzle. To implement them, Python (version 3) is chosen. The source code is attached with the this report. To further run the source code, the whole project is uploaded in github. The following sections of this report describe the basic understanding of the heuristics used, and provide comparative analysis based on the results found running the source code on several test cases.

\section{Description of 3 heuristics used}
\subsection{Uniform Cost Search}
When the algorithm attempts to choose which one of the current nodes in the queue is to be expanded, according to $A^{*}$ search, the algorithm calculates a cost function adding the current cost $g(n)$ and the heuristic cost $h(n)$. $h(n)$ is considered to be zero for Uniform Cost Search approach.

\subsection{$A^{*}$ search with Misplaced Tiles}
When the algorithm attempts to choose which one of the current nodes in the queue is to be expanded, according to $A^{*}$ search, the algorithm calculates a cost function adding the current cost $g(n)$ and the heuristic cost $h(n)$. $h(n)$ is considered to be the total count of the misplaced tiles in the current orientation excluding the tile numbered zero as it is the blank grid of the given matrix.

\begin{table}[!htb]
    \caption*{Misplaced Tiles Heuristic Example}
    \begin{minipage}{.5\linewidth}
      \caption*{Goal State}
      \centering
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            4 & 5 & 6 \\
            \hline
            7 & 8 & 0 \\
          \hline
          
        \end{tabular}
    \end{minipage}%
    \begin{minipage}{.5\linewidth}
      \centering
        \caption*{Current State}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            \textbf{8} & \textbf{7} & 6 \\
            \hline
            \textbf{5} & \textbf{4} & 0 \\
          \hline
          
        \end{tabular}
    \end{minipage} 
\end{table}

In the given example above, the heuristic will find that the current state has $h(n) = 4$ because the four bold tiles in the current state are not matched with the goal state.

\subsection{$A^{*}$ search with Manhattan Distance}
When the algorithm attempts to choose which one of the current nodes in the queue is to be expanded, according to $A^{*}$ search, the algorithm calculates a cost function adding the current cost $g(n)$ and the heuristic cost $h(n)$ based on the Manhattan Distance between the tiles which are not in order with the goal state. Manhattan Distance between two grid in a matrix is the sum of the absolute value of the difference of the row indices and column indices excluding the tile numbered zero as it is the blank grid of the given matrix.

\begin{table}[!htb]
    \caption*{Misplaced Tiles Heuristic Example}
    \begin{minipage}{.5\linewidth}
      \caption*{Goal State}
      \centering
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            4 & 5 & 6 \\
            \hline
            7 & 8 & 0 \\
          \hline
          
        \end{tabular}
    \end{minipage}%
    \begin{minipage}{.5\linewidth}
      \centering
        \caption*{Current State}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            \textbf{8} & \textbf{7} & 6 \\
            \hline
            \textbf{5} & \textbf{4} & 0 \\
          \hline
          
        \end{tabular}
    \end{minipage} 
\end{table}

In the given example below, the heuristic calculates the Manhattan distance for the Misplaced tiles (bold faced in the example). $h(n) = 2 (tile number\ 8) + 2(7) + 1(5) + 1(4) = 8$

\section{Comparisons among 3 heuristics used}

\subsection{Test cases used for the experiment results}
The project implementation considers the test cases provided in the project description.
\begin{table}[!hbt]
    \caption*{Depth of solution to test cases \{0, 2, 4, 8, 12, 16, 20, 24\} left to right}
\begin{tabular}{cccccccc}
    \begin{minipage}{0.1\linewidth}
        
        \begin{tabular}{|l|l|l|}
         
          \hline
            1 & 2 & 3 \\
           \hline
            4 & 5 & 6 \\
            \hline
            7 & 8 & 0 \\
          \hline
          
        \end{tabular}
        
    \end{minipage} &

    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            4 & 5 & 6 \\
            \hline
            0 & 7 & 8 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 2 & 3 \\
           \hline
            5 & 0 & 6 \\
            \hline
            4 & 7 & 8 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 3 & 6 \\
           \hline
            5 & 0 & 2 \\
            \hline
            4 & 7 & 8 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 3 & 6 \\
           \hline
            5 & 0 & 7 \\
            \hline
            4 & 8 & 2 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            1 & 6 & 7 \\
           \hline
            5 & 0 & 3 \\
            \hline
            4 & 8 & 2 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            7 & 1 & 2 \\
           \hline
            4 & 8 & 5 \\
            \hline
            6 & 3 & 0 \\
          \hline
          
        \end{tabular}
    \end{minipage} &
    
    \begin{minipage}{.1\linewidth}
        \begin{tabular}{|l|l|l|}
          \hline
            0 & 7 & 2 \\
           \hline
            4 & 6 & 1 \\
            \hline
            3 & 5 & 8 \\
          \hline
          
        \end{tabular}
    \end{minipage}
    
\end{tabular}
\end{table}

\subsection{Execution Time vs Depth}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{execution_time_vs_depth.png}
  \caption{A comparison of 3 heuristics on the Eight Puzzle Problem increasing solution depth}\label{fig:figure1}
\end{figure}
\begin{itemize}
    \item As Figure 1 suggests that for uniform cost search, the execution time is exponentially increasing as the depth of the solution increases.
    \item In case of other two heuristics, $A^{*}$ search with Manhattan Distance is faster than $A^{*}$ search with Misplaced tiles. 
\end{itemize}


\subsection{Node count (expanded) vs Depth}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{node_count_vs_depth.png}
  \caption{A comparison of 3 heuristics on the Eight Puzzle Problem for increasing solution depth}\label{fig:figure2}
\end{figure}

\begin{itemize}
    \item As Figure 2 suggests that for uniform cost search, the number of node count expanded is exponentially increasing as the depth of the solution increases.
    \item In case of other two heuristics, $A^{*}$ search with Manhattan Distance does not usually expand as much as nodes expanded in case of $A^{*}$ search with Misplaced tiles.
\end{itemize}

\subsection{Maximum queue size vs Depth}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{maximum_queue_vs_depth.png}
  \caption{A comparison of 3 heuristics on the Eight Puzzle Problem for increasing solution depth}\label{fig:figure3}
\end{figure}

\begin{itemize}
    \item As Figure 3 suggests that for uniform cost search, the maximum queue size during the search at any time is exponentially increasing as the depth of the solution increases.
    \item In case of other two heuristics, $A^{*}$ search with Manhattan Distance does not usually have as much as nodes in the queue in case of $A^{*}$ search with Misplaced tiles.
\end{itemize}

\subsection{Execution time vs Node count (expanded)}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{execution_time_vs_node_count.png}
  \caption{A comparison of 3 heuristics on the Eight Puzzle Problem for increasing node count}\label{fig:figure4}
\end{figure}

\begin{itemize}
    \item As Figure 4 suggests that for uniform cost search, the execution time   is linearly increasing as the number of node count expanded during the search increases.
    \item In case of other two heuristics, $A^{*}$ search with Manhattan Distance needs less execution time than $A^{*}$ search with Misplaced tiles, since $A^{*}$ search with Manhattan Distance does not usually have as much as nodes expanded as that of $A^{*}$ search with Misplaced tiles because of heuristic cost calculated.
\end{itemize}

\subsection{Maximum queue size vs Node count}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{maximum_queue_vs_node_count.png}
  \caption{A comparison of 3 heuristics on the Eight Puzzle Problem for increasing node count expansion}\label{fig:figure5}
\end{figure}

\begin{itemize}
    \item As Figure 5 suggests that for uniform cost search, the maximum queue size at any instant of the search is linearly increasing as the number of node count expanded during the search increases.
    \item In case of other two heuristics, $A^{*}$ search with Manhattan Distance finds smaller queue size than $A^{*}$ search with Misplaced tiles at any instant, since $A^{*}$ search with Manhattan Distance does not usually have as much as nodes expanded as that of $A^{*}$ search with Misplaced tiles because of heuristic cost calculated.
\end{itemize}


\section{Instructions to run the source code}
The source is uploaded https://github.com/mmasu012/Eight-Puzzle. There is a jupyter notebook which can be run to test the implementation. There is another file to generate the plots used for analysis across 3 heuristics discussed in the report.

\section{Results of the experiment}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{1.png}
  \caption{Results for depth 0, 2, 4}\label{fig:figure2}
\end{figure}

\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{2.png}
  \caption{Results for depth 8, 12, 16}\label{fig:figure2}
\end{figure}
\begin{figure}[!h]
  \centering
  \includegraphics[width=0.3\columnwidth]{3.png}
  \caption{Results for depth 20, 24}\label{fig:figure2}
\end{figure}

\section{Conclusion}
\begin{itemize}
    \item Eight puzzle problem needs huge computation power when the solution depth is bigger.
    \item Manhattan distance heuristic performs better than the Misplaced Tiles heuristics in respect of space and time complexities.
    \item Uniform cost search needs a huge amount of execution time for solution depth 16 20 and 24. 
    \item Manhattan distance can work for all the test cases in a very short execution time, where as when the depth is 24, even misplaced tiles needs huge amount of time.
    \item Due to taking more amount of execution time, the comparative analysis presents for the testcases with solution depth upto 12.
    \item All the statistics experimented from solution depth 0 to depth 24 have been attached in the report. 
\end{itemize}


\end{document}


