**Security Operations Hub**
A comprehensive web-based platform designed for security operations teams, providing integrated tools for query management, threat intelligence analysis, and indicator of compromise extraction. Built with modern web technologies, the platform combines operational efficiency with advanced security analysis capabilities.

**Overview**
The Security Operations Hub serves as a centralized workspace for security analysts and SOC teams, offering three primary operational tools alongside analytics dashboards and administrative features. The application is designed with both functionality and user experience in mind, featuring a responsive interface with elegant theming and comprehensive audit logging capabilities.

**Core Features**
**Quick Query Manager**
The Quick Query Manager provides a centralized repository for frequently used Kusto Query Language queries, specifically designed for Microsoft Sentinel and Azure Data Explorer environments. Security analysts can save, categorize, and retrieve queries with associated metadata including descriptions, categories, and timestamps. Each query entry maintains full query syntax with proper formatting, allowing for quick copy-to-clipboard functionality that streamlines the investigation workflow. The manager supports query organization through categorical grouping, making it simple to locate relevant queries during time-sensitive security incidents. Users can add new queries through an intuitive form interface, edit existing entries, and delete outdated queries as operational needs evolve.

**Threat Intelligence Lookup**
The Threat Intelligence Lookup tool aggregates data from multiple reputable threat intelligence sources to provide comprehensive analysis of indicators of compromise. The tool supports multiple indicator types including IPv4 and IPv6 addresses, domain names, URLs, file hashes, and email addresses. When an analyst submits an indicator for investigation, the system queries VirusTotal for malware detection statistics and community reputation scores, retrieves geolocation data and WHOIS information for IP addresses, checks AbuseIPDB for abuse reports and confidence scores, queries AlienVault OTX for associated threat pulses and malware families, and optionally queries IPQualityScore for fraud detection and proxy identification.

The results are presented in a structured format with dedicated cards for each intelligence source, expandable sections for detailed data examination, and direct links to view full reports on each provider's platform. A standout feature is the Incident Notes Summary, which correlates all intelligence findings into a professionally formatted narrative suitable for SOC documentation. These summaries include defanged indicators for safe sharing, timestamp information, comprehensive risk assessments, and recommended actions based on the aggregated intelligence. The notes are presented in a terminal-style interface with one-click copy functionality, allowing analysts to quickly document findings in ticketing systems or case management platforms.

The tool implements automatic indicator defanging, converting potentially dangerous indicators into safe representations by replacing periods with brackets and modifying URL protocols. This prevents accidental clicks on malicious links while maintaining indicator readability. For IP addresses, the system displays country flags and interactive world map markers showing geolocation data. When WHOIS data is unavailable or IPQS API credits are exhausted, the system gracefully handles these scenarios with appropriate messaging and manual lookup options.

**IOC Scraper**
The IOC Scraper automates the extraction of indicators of compromise from threat intelligence articles, research reports, and security bulletins. Analysts can paste article content or provide URLs, and the tool employs sophisticated pattern matching to identify and extract various indicator types including IP addresses both IPv4 and IPv6, domain names and subdomains, URLs with various protocols, file hashes in MD5, SHA1, and SHA256 formats, email addresses, and CVE identifiers.

The extracted indicators are organized by type and presented in a clean, structured format with visual grouping and color coding. Each indicator type appears in its own section with appropriate icons and styling. Indicators are automatically defanged for safe handling and sharing, and the interface provides one-click copy functionality for individual indicators or entire categories. The tool handles complex text formats, filters out false positives, and maintains proper formatting even when processing lengthy documents or multiple articles simultaneously.

**IOC Refanging Tool**
Complementing the scraper functionality, the IOC Refanging Tool converts defanged indicators back to their original operational format. This is particularly useful when analysts need to submit indicators to security tools or perform active investigations. The tool processes defanged IPs, domains, URLs, and email addresses, restoring them to proper syntax with visual formatting that uses bold colors and clear presentation. The refanging process is instant, and results are displayed in an easily copyable format with black text for optimal readability.

**Analytics and Monitoring**
The platform includes comprehensive analytics dashboards that provide visibility into operational activities. The system tracks query usage patterns, threat intelligence lookup frequencies, IOC scraper utilization, and user activity trends over time. These metrics help security teams understand their operational patterns, identify commonly investigated threat types, and optimize their workflows based on actual usage data.

The Audit Log Viewer provides administrators with detailed visibility into system access and usage. Every user interaction is logged with timestamps, IP addresses, user agents, and activity descriptions. The audit system tracks successful and failed authentication attempts, query management operations, threat intelligence lookups, IOC scraper usage, and administrative actions. Logs are retained for three days with a clear visual indicator of this retention policy, and the interface supports filtering and searching to quickly locate specific events during security reviews or compliance audits.

**Additional Features**
Interactive Games Suite
The platform includes a collection of sophisticated games accessible through a stylish floating menu in the top-right corner of the interface. Each game features smooth page transitions, hover animations, and integrated leaderboard systems. The Snake game offers both manual play and an autonomous bot mode featuring Steven Bosh, an AI player that uses greedy pathfinding with collision avoidance. The bot prioritizes safe moves toward food using Manhattan distance calculations and wall detection, playing at a measured 120ms interval for watchability.

The Tetris implementation includes an advanced bot player that achieves near-perfect gameplay through breadth-first search evaluation of board positions. The bot analyzes aggregate height, holes, bumpiness, complete lines, and well depth using optimized weights derived from genetic algorithms. It evaluates all possible rotations and positions for each piece, selecting optimal placements that maximize line clearing potential while minimizing stack height and holes.

The Minesweeper game offers four difficulty levels with a probability-based AI solver. The bot identifies certain mines and safe cells, calculates probabilities for ambiguous positions, and strategically prefers corner and edge moves during early game phases. The Tic-Tac-Toe game features a minimax algorithm implementation with alpha-beta pruning for optimal computer opponent behavior.

All games include leaderboard systems that track high scores and completion times, with scores persisted to the database and displayed in ranked format with medal indicators for top performers. Both human players and bot performances are tracked, allowing for interesting comparisons between human and AI capabilities.

**Technical Implementation**
**Frontend Architecture**
The application is built using Next.js 14 with React 18, leveraging the App Router architecture for optimal performance and server-side rendering capabilities. The component library is based on Radix UI primitives, providing accessible and customizable interface elements. Styling is implemented through Tailwind CSS with custom theme extensions, enabling consistent design language across the platform. Framer Motion powers the animation system, delivering smooth transitions, entrance animations, and interactive feedback throughout the interface.

The theming system supports both light and dark modes through next-themes, with careful attention to contrast ratios and readability in both modes. The Christmas theme implementation demonstrates advanced animation capabilities with falling snowflakes using randomized paths and durations, twinkling lights with staggered pulse animations, and subtle gradient overlays with animated glow effects. All animations are performant, using CSS transforms and opacity changes to avoid layout thrashing.

**Backend Infrastructure**
The backend is built on Next.js API routes, providing serverless function endpoints for all data operations. These routes handle authentication verification, query CRUD operations, threat intelligence aggregation, IOC extraction processing, game score management, and audit log creation and retrieval. Each endpoint implements proper error handling with appropriate HTTP status codes, request validation to prevent malformed data, and audit logging for security monitoring.

The database layer uses Prisma ORM with PostgreSQL, providing type-safe database access with compile-time query validation. The schema includes models for user authentication with passkey support, saved queries with categorical organization, game scores across all game types with difficulty tracking, and comprehensive audit logs with IP and user agent tracking. Database indexes are strategically placed on frequently queried fields to ensure optimal performance even as data volumes grow.

**External Integrations**
The threat intelligence system integrates with multiple external APIs through secure credential management. VirusTotal integration provides malware detection data and community reputation scores. AbuseIPDB integration delivers abuse report aggregation and confidence scoring. AlienVault OTX integration supplies threat pulse data and malware family associations. IPQualityScore integration offers fraud detection and proxy identification with optional opt-in functionality.

API credentials are securely stored and managed through environment variables with proper access controls. The system implements graceful degradation when API limits are reached or services are unavailable, ensuring analysts can continue working with available data sources. Rate limiting is respected through proper request throttling, and error responses are handled with user-friendly messaging that explains service status.

**Security Considerations**
The platform implements passkey authentication for passwordless, phishing-resistant user verification. All database operations use parameterized queries through Prisma to prevent SQL injection attacks. Indicators of compromise are automatically defanged throughout the interface to prevent accidental activation of malicious links. Comprehensive audit logging tracks all system access and operations for security monitoring and compliance purposes. API credentials are never exposed to client-side code, remaining securely server-side throughout all operations.

**Performance Optimization**
The application employs React Server Components for optimal initial page loads, code splitting to reduce bundle sizes, image optimization through Next.js Image component, and memoization of expensive computations in game AI algorithms. Database queries are optimized with appropriate indexes and selective field retrieval. The frontend implements debouncing on search inputs, lazy loading of heavy components, and efficient state management to minimize re-renders.

**Deployment**
The application is designed for deployment on modern serverless platforms with support for Next.js applications. Environment variables configure database connections, API credentials, and feature flags. The build process includes TypeScript compilation with strict type checking, production bundle optimization, and static page generation where applicable. The platform is currently deployed at secops.abacusai.app, providing secure, scalable access for security operations teams.
