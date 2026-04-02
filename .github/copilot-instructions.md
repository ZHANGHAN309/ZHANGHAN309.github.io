# Project Guidelines

## Architecture
This is a Hexo static blog site using the ParticleX theme. Content is in `source/_posts/` organized by categories. Generated site in `public/`.

## Build and Test
- Install: `npm install`
- Build: `npm run build` (hexo generate)
- Serve locally: `npm run server` (hexo server)
- Clean: `npm run clean`
- Deploy: `npm run deploy` or push to master for GitHub Actions auto-deploy

## Conventions
- Posts use YAML front matter with title, date, tags
- Categories: Android, CMake, CS, JavaScript, PLC, etc.
- Custom styles in `source/css/custom.css`
- Theme config in `themes/particlex/_config.yml`

See [themes/particlex/README.md](themes/particlex/README.md) for theme details.
See [source/_posts/如何搭建博客-具体流程.md](source/_posts/如何搭建博客-具体流程.md) for setup guide.